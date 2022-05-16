# Deploy Azure Databricks models in Azure Machine Learning

## Describe consideration for model deployment

**Model deployment** is a process where the trained ML models is interated into a production environment such that end users can use the model predictions to make decisions or gain insight into data.

**Real-time inferencing** is when the model is deployed as part of a service that enables applications to request immediate or *real-time8 predictions for individual or small numbers of data observations.

In AML, real0time inferencing solution can be deployed as a real-time service hosted in a containerized platform such as Azure Kubernetes Service (AKS)

## Plan for AML deployment endpoints

The service components and tools can be used to register the model and deploy it to one of the **available compute target** so it can be made available as a web service in Azure cloud.

Available compute target:

| Compute target | Usage | Description |
| --- | --- | ---|
| Local web service | Testing/debug | Good for limited testing and troubleshooting. |
| Azure Kubernetes Service (AKS) | Real-time inference | Good for high-scale production deployments. Provides autoscaling, and fast response times. |
| Azure Container Instances (ACI) | Testing | Good for low scale, CPU-based workloads. |
| Azure Machine Learning Compute Clusters | Batch inference | Run batch scoring on serverless compute. Supports normal and low-priority VMs. |
| Azure IoT Edge | (Preview) IoT module | Deploy & serve ML models on IoT devices. |

## Deploy a model to AML

AML uses containers as a deployment mechanism, packaging the model and the code to use it as an image that can be deployed to a container in your chosen compute target.

To deploy a model as an inferencing webservice, these task need to be performed:
1. Register a trained model

        from azureml.core import Model

        model = Model.register(workspace=ws, 
                            model_name='nyc-taxi-fare',
                            model_path='model.pkl', # local path
                            description='Model to predict taxi fares in NYC.')
2. Define an Inference Configuration: model will be deployed as a service that consists of
    - A script to load the model and return the predictions for summited data. The *entry script* for the service as a `.py` file that include 2 function
        - **init()**: called when the service is initialized
        - **run(raw_data)**: called when new data is summited to the service

                import json
                import joblib
                import numpy as np
                from azureml.core.model import Model

                # Called when the service is loaded
                def init():
                    global model
                    # Get the path to the registered model file and load it
                    model_path = Model.get_model_path('nyc-taxi-fare')
                    model = joblib.load(model_path)

                # Called when a request is received
                def run(raw_data):
                    # Get the input data as a numpy array
                    data = np.array(json.loads(raw_data)['data'])
                    # Get a prediction from the model
                    predictions = model.predict(data)
                    # Return the predictions as any JSON serializable format
                    return predictions.tolist()

    - An environment in which the scipt will be run. AML environment are an encapsulation of the environment where ML training happens. Python packages, env variable, docker settings and other attributes can be declared.

            from azureml.core import Environment
            from azureml.core.environment import CondaDependencies

            my_env_name="nyc-taxi-env"
            myenv = Environment.get(workspace=ws, name='AzureML-Minimal').clone(my_env_name)
            conda_dep = CondaDependencies()
            conda_dep.add_pip_package("numpy==1.18.1")
            conda_dep.add_pip_package("pandas==1.1.5")
            conda_dep.add_pip_package("joblib==0.14.1")
            conda_dep.add_pip_package("scikit-learn==0.24.1")
            conda_dep.add_pip_package("sklearn-pandas==2.1.0")
            myenv.python.conda_dependencies=conda_dep

            from azureml.core.model import InferenceConfig

            from azureml.core.model import InferenceConfig
            inference_config = InferenceConfig(entry_script='score.py', 
                                            source_directory='.', 
                                            environment=myenv)
3. Define a Deployment Configuration: after entry script and environment, the compute which the service will be deployed need to be configured. If AKS cluster is the compute target
    - Create the cluster before deploying

            from azureml.core.compute import ComputeTarget, AksCompute

            cluster_name = 'aks-cluster'
            compute_config = AksCompute.provisioning_configuration(location='eastus')
            production_cluster = ComputeTarget.create(ws, cluster_name, compute_config)
            production_cluster.wait_for_completion(show_output=True)

    - Define the deployment configuration. which set the target-specific compute specification for the containerized deployment

            from azureml.core.webservice import AksWebservice

            deploy_config = AksWebservice.deploy_configuration(cpu_cores = 1,
                                                            memory_gb = 1)

4. Deploy the Model: call the deploy method of the model class. For ACI or local services, omit the `deployment_target` parameter

        from azureml.core.model import Model

        service = Model.deploy(workspace=ws,
                            name = 'nyc-taxi-service',
                            models = [model],
                            inference_config = inference_config,
                            deployment_config = deploy_config,
                            deployment_target = production_cluster)
        service.wait_for_deployment(show_output = True)

## Troubleshoot model deployment

1. Check the service state: for operational service, the state should be *Healthy*

        from azureml.core.webservice import AksWebservice

        # Get the deployed service
        service = AksWebservice(name='classifier-service', workspace=ws)

        # Check its state
        print(service.state)

2. Review service log: if the service is NOT healthy, or error happens, logs can be reviewed

        print(service.get_logs())

3. Deploy to a local container: local container service can be used to diagnose runtime error

        from azureml.core.webservice import LocalWebservice

        deployment_config = LocalWebservice.deploy_configuration(port=8890)
        service = Model.deploy(ws, 'test-svc', [model], inference_config, deployment_config)

        print(service.run(input_data = json_data))

        # can only reload without redeploying on local service
        service.reload()
        print(service.run(input_data = json_data))


## Summary

- Describe considerations for model deployments
- Plan for deployments endpoints
- Deploy a model as an inderencing webservice
- Troubleshoot model deployment