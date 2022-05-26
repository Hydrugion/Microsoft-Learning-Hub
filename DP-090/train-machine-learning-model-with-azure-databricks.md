# Train a machine learning model with Azure Databricks

## Understand Spark ML

One library, two approaches: MMLib and SparkML
- MLLib: is a legacy approach for ML in Spark. From Spark 2.0 it entered maintainance.
- SparkML: primary approach, support Dataframe APIs and classic RDD approach.

## Train and validate a model

Process:
- Splitting data: between training and validation set. Dataframe support `randomSplit()` function
- Training a model
- Validating a model

A training model relies on 3 key abstraction: *transformer, estimator* and *pipeline*
- Transformer input a Dataframe and output a new Dataframe. Implement `transform()` method
- Estimator input a Dataframe and output a model, which is itself a transformer. Implement `fit()` method.
- Pipeline combine together estimators and transformer and implement a `fit()` method

After trained, a model can be validated using `summary` object
- Based on training data
- With a validation dataset, we can run the `transform()` function using it as the input and get the summary statistic on never-seen data.

## Using other ML framework

Best to use the Databricks Runtime for Machine Learning. Pre-installed includes TensorFlow, Pytorch, Keras, XGBoost. Also includes essential libraries for distributed training. For library that does not support distributed training, it is possible to use a single node cluster.

## Summary

- Describe SparkML
- Train and validate a machine learning model
- Use other ML framework