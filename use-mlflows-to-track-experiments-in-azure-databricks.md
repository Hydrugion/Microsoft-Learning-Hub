# Use MLflow to track experiments in Azure Databricks

When doing machine learning task in Azure Databricks, MLflow can be used to track and review the works.

## Understand capabilities of MLflow

MLFlow is an open-sourced product designed to manage ML development cycle. Allow data scientists to train models, register those models, deploy the models to a web-server and manage model updates.

Four components:
- MLflow Tracking: allows DS to work with experiments. For each run, parameters, versions, evaluation metrics and generated output can be logged.
- MLflow Projects: a way of packing code in a manner, allow for consistent deployment and reproduce the result. Support several environments for project, including Conda, Docker, and directly on system
- MLflow Models: standarized format for packaging model for distribution. Allows MLflow to work with model from several popular lib including sklearn, keras, mllib, onnx and more
- MLflow Model Registry: register model in a registry. allows operations team members to deploy models in the registry and serving the either through a  REST API or as part of a batch inference solution

## Use MLflow terminology

**MLflow tracking**: built around **runs** which is executions of code for a DS task. Each runs contains some key attributes:
- Parameters: key-value pairs that represent inputs. Used to track hyperparameters of the model
- Metrics: key-value pair that represent how the model is performing. Can be updated theroughout the course of a run.
- Artifacts: Output files in any format, models, images, log files, data files that might be important for model analysis and understanding

**Runs** can be combined into **experiments**, which DS can later review and determine the best generated model

**MLflow projects**: a method of packaging DS code. Allows automated processes to use the code in consistenct manner. Each project includes at least one *entry point* (wither a .py or .sh) that is intended for the starting point for project use. Projects also specify details about *environment* which includes specific packages and their version used.

**MLflow models**: is a directory containing an abritary set of files along with an **MLmodel** file in the root directory. MLflow allows model to be of a particular *flavor*, which is a descriptor of which tool or libary generated the model. Each model has a *signature* which describe the expected inputs and outputs for the model.

**MLflow model registry**: keep track of a model from MLflow Model. the DS *registers* a model with the Model REgistry, storing details such as the name. Each registered model mayhave multiple *versions* which allow DS to keep track of model changes over time. It is also possible to *stage* model. Each model can be in one stage *Staging*, *Production*, *Archived*. DS and admins may *transition* a model version from one stage to next.

## Run experiments

Useful for comparing changes over time or comparing relative performance of models with different hyperparameters.

Example

    with mlflow.start_run():
        mlflow.log_param("input1", input1)
        mlflow.log_param("input2", input2)
        # some model training here
        mlflow.log_metric("rmse", rmse)

In this case the experiment's name will be the name of the notebook. It is possible export a variable named `MLFLOW_EXPERIMENT_NAME` to change the name of the experiment.

**Reviewing experiments**: Inside a notebook, the Experiment menu option display a context bar, which includes information on runs of the current experiment. Selecting External Link will provide additional details on a particular run.

## Summary

- Describe capabilities of MLflow
- Describe MLflow terms
- Start a run in MLflow