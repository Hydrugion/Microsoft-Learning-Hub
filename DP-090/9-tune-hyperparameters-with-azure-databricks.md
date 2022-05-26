# Tine hyperparameters with Azure Databricks

## Understand hyperparameters tuning

Hyperparameter tuning: process of choosing model parameters which produce the best result on loss function after training

Cross validation: prevent hyperparameter overfitting by training and validate multiple model on different part of training set.

## Automated MLflow for model tuning

ADB for ML suppor automated MLflow tracking, where hyperparameter values and evaluation are automatically logged in MLflow and a hierarchy will be created for the different runs that represent the distinct models you train.

To use automatd MLflow tracking:
- Use a Python notebook to host the code
- Attach the notebook to a cluster with Databricks runtime or Databricks runtime for ML
- Setup hyperparameter tuning with CrossValidator or TrainValidationSplit

MLflow will automatically create a parent run that contains the information for the method and child runs that are nested under the parent run. Each child run represent a trained model and hyperparameter values and resulting evaluation metrics used can be seen.

Run tuning code:
- List the available hyperparameters

        print(lr.explainParams())

- Setup the search space and sampling method

from pyspark.ml.tuning import ParamGridBuilder

        paramGrid = (ParamGridBuilder()
        .addGrid(lr.maxIter, [1, 10, 100])
        .addGrid(lr.fitIntercept, [True, False])
        .addGrid(lr.standardization, [True, False])
        .build()
        )

- Run the code with automated MLflow

        from pyspark.ml.evaluation import RegressionEvaluator
        from pyspark.ml.tuning import CrossValidator

        evaluator = RegressionEvaluator(
        labelCol = "medv", 
        predictionCol = "prediction"
        )

        cv = CrossValidator(
        estimator = pipeline,             # Estimator (individual model or pipeline)
        estimatorParamMaps = paramGrid,   # Grid of parameters to try (grid search)
        evaluator=evaluator,              # Evaluator
        numFolds = 3,                     # Set k to 3
        seed = 42                         # Seed to sure our results are the same if ran again
        )

        cvModel = cv.fit(trainDF)


        bestModel = cvModel.bestModel

## Hyperparameter tuning with Hyperopt

When training a Python model, follow these steps:

1. Define objective function to **minimize**

        from sklearn.model_selection import cross_val_score
        from sklearn.svm import SVC

        def objective(C):
            clf = SVC(C)
            
            accuracy = cross_val_score(clf, X, y).mean()
            
            return {'loss': -accuracy, 'status': STATUS_OK}

2. Define hyperparameters seach space
    - `hp.choice(label, options)`
    - `hp.randint(label, upper)`
    - `hp.uniform(label, low, high)`
    - `hp.normal(label, mu, sigma)`
3. Specify search algorithm
    - `hyperopt.tpe.suggest`
    - `hyperout.rand.suggest`
4. Run the Hyperopt function fmin()
    - `fn`: the objective function
    - `space`: search space
    - `algo`: search algorithm
    - `max_evals`: max model to train
    - `max_queue_len`: number of hyperparams to generate beforehand
    - `trails`: `SparkTrials` or `Trials` objects. When using `SparkTrials` or Horovod, automated MLflow tracking is enabled.

## Summary

- Describe hyperparameters tuning
- Use automated MLflow for hyperparameter tuning
- Use Hyperopt for hyperparameter tuning