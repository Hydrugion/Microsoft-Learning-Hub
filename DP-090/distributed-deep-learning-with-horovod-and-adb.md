# Distributed deep learning with Horovod and Azure Databricks

Learn how to distributed deep learning with HorovodRunner

## Understand Horovod

Help DS with training deep learning model. 

Deep learning quick review:
- Subfield of ML
- Model consists of layers. Training process start with data sumbitted in batches
- The data is passed between layer until it reaches the output layer and produce a prediction. It is then compared to the ground truth and the model can be updated accordingly
- The model is trained over multiple iteration called **epochs**

ADB can train deep learning model using popular opensourced project like pyTorch, TensorFlow, Keras. When we use these we should use a single node cluster in in ADB.

Because deep learning scale well with large amout of data, the data might not fit in a single node cluster and need to be trained distributedly

Horovod is an open sourced distributed training framework and an alternative solution to training model on a single node cluster. Horovod makes use of Spark's parallelism to distribute the training process.

When used on top of the popular deep learning framework, it trains multiple models on different batches of the input dataset on separate worker. At the end of each epoch, weights are communicated between workers and the average weight of all worker is calculated. The cycle is repeat.

## HorovodRunner for distributed deep learning

HorovodRunner is a general API which triggers Horovod jobs. 

**Horovod process**: To distribute a training of a deep learning model
1. Prepare and test single node code: Make sure to warp the main training procedure into 1 function which is later be used for distributed execution.
2. Migrate the code to Horovod
    1. Import the Horovod framework `hvd`
    2. Initialize the library `hvd.init()`
    3. Pin 1 GPU per processes. Skip this when using CPUs
    4. Specify the data partition to use. Best practice to keep the parititon size similar
    5. Scale the learning rate by the number of workers to make sure the sum of weights are calculated correctly after each epoch
    6. Use Horovod distributed optimizer to handle communication between workers
    7. Broadcast the initial parameters to all worker
    8. Save checkpoints only on worker 0
3. Use HorovodRunner to run the code: Create a `HorovodRunner` instances and specify the number of training node using `np` params (to test on single node use -1). Finally trigger the training job by invoking the python function created for training jobs.

## Summary

- Understand what Horovod is and how it helps distribute the training of deep learning models
- Use HorovodRunner in Azure Databricks for distributed deep learning