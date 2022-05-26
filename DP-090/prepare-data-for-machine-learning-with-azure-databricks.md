# Prepare data for machine learning with Azure Databricks

## Understand ML concepts

Machine learning is a data science technique to extracts pattern from data allowing the computers to identify related data, forecast outcomes, behaviours and trend.

ML as the new programing paradigm:
- `TraditionalPrograming(Rules, Data) -> Answers`
- `MachineLearning(Answers, Data) -> Rules`

## Perform data cleaning

Data cleaning deals with issue in data quality such as errors, missing values and outliers.

**Imputation of null value**: Null refers to unknown or missing data. Strategy includes:
- Dropping the records
- Adding placeholder
- Basic imputing: fill null with "best guess" mean or median for numerial and most frequent value for categorical
- Advanced imputing: advanced method for determine "best guess" such as clustering algorithm or oversampling technique

**Converting data types**: when the columns have inconsistence/mixed data types

**Duplicate records**: easiest solution is to drop the duplicate record

**Outliers**: outliers are observations that significantly different to all other observations. Common approach includes compute Z-score of a column.

## Perform feature engineering

ML models are as strong as the data they are trained on. It is important to derive features from existing raw data that better represent the nature of data and help impove the predictive power of the machine learning algorithm.

**Feature engineering**: process of generating new predictive feature from existing raw data. Common approaches:
- Aggregation: count, sum, average, mean, median
- Part-of
- Binning
- Flagging
- Frequency-based
- Embedding
- Deriving by example
- Domain-based approach

## Perform data scaling

Range of value between feature varies and some ML algorithm are very sensitive to magnitude of input feature. Common approaches:
- Normalization: rescales the data into [0, 1] using math
- Standardization: rescahe the data to have mean = 0 and standard deviation = 1

## Perform data encoding

In ML, we ultimately work with number only (or vectors to be precise). Categorical or discrete data need to be encoded into number. Common approaches:
- Ordinal encoding: map each discrete value into a number
- One hot encoding: transform the value into binary-column format

## Sumary

- Describe concepts of machine learning
- Perform data cleaning
- Perform feature engineering
- Perform data scaling
- Perform data encoding
