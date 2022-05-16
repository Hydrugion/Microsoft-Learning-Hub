# Manage machine learning model in Azure Databricks

Learn how to to use MLFlow in Azure Databricks to register and manage models.

## Describe consideration for model management

Two key steps for model management in MLFlow are **registration** and **versioning**.

Registration is simply store the name and details of a model onto **MLFlow Model Registry**.

MLFlow versioning system makes model management easy by labeling new versions of the models and retaining the information of prior model versions automatically.

## Register model

2 ways through UI or code

Using the UI:
1. Start with an experiment run
2. On the details page, select the folder contains the model then select Register Model
3. If the model is not created before, select the dropdown list and choose *Create new model*
4. Set name for the new model and register

Using code:
1. One way is to register directly from an experiment

        model_details = mlflow.register_model(model_uri=model_uri, name=model_name)
2. Another way is to register during a run by naming `registered_model_name`

        with mlflow.start_run() as run:
            mlflow.log_params("param1", 123)
            mlflow.sklearn.log_model(
                sk_model=model,
                artifact_path="model",
                registered_model_name="sklearn Trained Model")

After registration, the model can be referenced using

    model = mlflow.sklearn.load_model(
        model_uri=f"models:/{model_name}/{model_version}")

Registering a model is important:
- Allow MLFlows and ADB to keep track of the model
- **Allow serving the model for real-time or batch scoring automatically**
- Create new version overtime, track model changes and perform comparisons

## Manage model versioning

Versioning process using UI: same process as registration
1. Start with an experiment run
2. On the detail page, select the folder contains the model and select **Register Model**
3. Because the model is already registered, select the **Model** from the dropdown list
4. Select **Register** to complete versioning

Stage model version: In addition to versioning, MLFlow allows model versions to be in specfic stage
- **Production**: intended for deployment
- **Staging**: intended for testing
- **Archived**: nolonger intended for use

Model start with no stage, and it can be changed using UI and code:
- Using UI: select the version link and in the Stage and either request a transition or performing the transition.
- Using code:

        client.transition_model_version_stage(
            name=model_details.name,
            version=model_details.version,
            stage='Staging',
            )

Model after transition can be retrieved at a stage

    import mlflow.pyfunc
    model_uri = "models:/{model_name}/{model_stage}".format(model_name=model_name, model_stage=model_stage)
    model = mlflow.pyfunc.load_model(model_uri)

## Summary

- Describe consideration for model management
- Register model
- Manage model versioning