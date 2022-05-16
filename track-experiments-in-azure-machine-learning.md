# Track Azire Databricks experiments in Azure Machine Learning

AML is a scalable platform for training, deploying and managing ML solutions. AML can be integrated with ADB and MLFlow.

## Describe Azure Machine Learning

AML is a platform for operating ML workloads on the cloud.
- Scale on demandcompute for ML workloads
- Data storage and connectivity to ingest data from wide range of sources
- ML workflow orchestration to automate model training, deployment and management processes
- Model registration and management
- Metrics and monitoring for training experiments, dataset and published services
- Model deployment for real-time and batch inferencing

## Run ADB experiments in AML

1. Configure MLFlow tracking URI touse AML
    - Get AML workspace object
    - Get the unique tracking URI address from that object
    - Setup MLFlow tracking URI to point to AML workspace
2. Provice the name for MLFlow experiment
3. Run experiment

## Log metrics in AML with MLFlow

In MLFlow experiment:
- `mlflow.log_metric()` can be used to log the model's metric
- `mlflow.log_artifacts()` can be used to save model artifacts

Reviewing experiment metrics and artifacts in Azure ML Studio
- From **Experiments** tab, open the corresponding MLFlow experiment
- In the **Metrics** tab of the run, model metrics that were logged can be viewed
- In the **Outputs + logs** tabs, model artifacts can be viewed

## Run AML pipelines on ADB compute

AML support **multiple** types of compute for experimentation and training, including Databricks compute.

In AML, a pipeline is a workflow of ML tasks, which each tasks implemented as a *step*. Steps can be arranged sequencially or parallel and can be run on a specific compute target, make it possible to combine different types of processing as required to achieve an overall goal.

Running pipeline step on ADB compute:
- AML support a specialized pipeline step called DatabricksStep, in which a notebook, script or compiled JAR can be run on a ADB cluster.
- To use this step:
    1. Attack a ADB Compute to AML workspace

            from azureml.core import Workspace
            from azureml.core.compute import ComputeTarget, DatabricksCompute

            # Load the workspace from the saved config file
            ws = Workspace.from_config()

            # Specify a name for the compute (unique within the workspace)
            compute_name = 'db_cluster'

            # Define configuration for existing Azure Databricks cluster
            db_workspace_name = 'db_workspace'
            db_resource_group = 'db_resource_group'
            # Get the access token from the Databricks workspace
            db_access_token = '1234-abc-5678-defg-90...' 
            db_config = DatabricksCompute.attach_configuration(resource_group=db_resource_group,
                                                            workspace_name=db_workspace_name,
                                                            access_token=db_access_token)

            # Create the compute
            databricks_compute = ComputeTarget.attach(ws, compute_name, db_config)
            databricks_compute.wait_for_completion(True)
    2. Define DatabricksStep in a pipeline

            from azureml.pipeline.core import Pipeline
            from azureml.pipeline.steps import DatabricksStep

            script_directory = "./scripts"
            script_name = "process_data.py"

            dataset_name = "nyc-taxi-dataset"

            spark_conf = {"spark.databricks.delta.preview.enabled": "true"}

            databricksStep = DatabricksStep(name = "process_data", 
                                            run_name = "process_data", 
                                            python_script_params=["--dataset_name", dataset_name],  
                                            spark_version = "7.3.x-scala2.12", 
                                            node_type = "Standard_DS3_v2", 
                                            spark_conf = spark_conf, 
                                            num_workers = 1, 
                                            python_script_name = script_name, 
                                            source_directory = script_directory,
                                            pypi_libraries = [PyPiLibrary(package = 'scikit-learn'), 
                                                            PyPiLibrary(package = 'scipy'), 
                                                            PyPiLibrary(package = 'azureml-sdk'), 
                                                            PyPiLibrary(package = 'azureml-dataprep[pandas]')], 
                                            compute_target = databricks_compute, 
                                            allow_reuse = False
                                        )
    3. Submit the pipeline

            from azureml.pipeline.core import Pipeline
            from azureml.core import Experiment

            # Construct the pipeline
            pipeline = Pipeline(workspace = ws, steps = [databricksStep])

            # Create an experiment and run the pipeline
            experiment = Experiment(workspace = ws, name = "process-data-pipeline")
            pipeline_run = experiment.submit(pipeline)

## Summary

- Describe AML
- Run an experiment
- Log metrics with MLFlow
- Run pipeline step on Databricks Compute