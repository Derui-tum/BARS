## DeepIM_movielenslatest_x1

A hands-on guide to run the DeepIM model on the Movielenslatest_x1 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.6GHz
  GPU: Tesla P100 16G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 11.4
  python: 3.6.5
  pytorch: 1.0.1.post2
  pandas: 0.23.0
  numpy: 1.18.1
  scipy: 1.1.0
  sklearn: 0.23.1
  pyyaml: 5.1
  h5py: 2.7.1
  tqdm: 4.59.0
  fuxictr: 1.1.0
  ```

### Dataset
Dataset ID: [Movielenslatest_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/MovieLens/README.md#Movielenslatest_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/tree/v1.1.0) for this experiment. See the model code: [DeepIM](https://github.com/xue-pai/FuxiCTR/blob/v1.1.0/fuxictr/pytorch/models/DeepIM.py).

Running steps:

1. Download [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.0.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Movielens/MovielensLatest_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [DeepIM_movielenslatest_x1_tuner_config_01](./DeepIM_movielenslatest_x1_tuner_config_01). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd DeepIM_movielenslatest_x1
    nohup python run_expid.py --config ./DeepIM_movielenslatest_x1_tuner_config_01 --expid DeepIM_movielenslatest_x1_001_eb1c9e99 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

Total 5 runs:

| Runs | AUC | logloss  |
|:--------------------:|:--------------------:|:--------------------:|
| 1 | 0.969316 | 0.209861  |
| 2 | 0.967859 | 0.212252  |
| 3 | 0.968758 | 0.212782  |
| 4 | 0.967749 | 0.212312  |
| 5 | 0.968553 | 0.212095  |
| Avg | 0.968447 | 0.211860 |
| Std | &#177;0.00058242 | &#177;0.00102560 |


### Logs
```python
2022-02-10 13:47:48,824 P36078 INFO {
    "batch_size": "4096",
    "data_format": "csv",
    "data_root": "../data/Movielens/",
    "dataset_id": "movielenslatest_x1_cd32d937",
    "debug": "False",
    "embedding_dim": "10",
    "embedding_regularizer": "0.01",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['user_id', 'item_id', 'tag_id'], 'type': 'categorical'}]",
    "gpu": "0",
    "hidden_activations": "relu",
    "hidden_units": "[400, 400, 400]",
    "im_batch_norm": "True",
    "im_order": "5",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "DeepIM",
    "model_id": "DeepIM_movielenslatest_x1_001_eb1c9e99",
    "model_root": "./Movielens/DeepIM_movielenslatest_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_batch_norm": "True",
    "net_dropout": "0.3",
    "net_regularizer": "0",
    "num_workers": "3",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Movielens/MovielensLatest_x1/test.csv",
    "train_data": "../data/Movielens/MovielensLatest_x1/train.csv",
    "use_hdf5": "True",
    "valid_data": "../data/Movielens/MovielensLatest_x1/valid.csv",
    "verbose": "1",
    "version": "pytorch"
}
2022-02-10 13:47:48,827 P36078 INFO Set up feature encoder...
2022-02-10 13:47:48,827 P36078 INFO Load feature_map from json: ../data/Movielens/movielenslatest_x1_cd32d937/feature_map.json
2022-02-10 13:47:48,828 P36078 INFO Loading data...
2022-02-10 13:47:48,837 P36078 INFO Loading data from h5: ../data/Movielens/movielenslatest_x1_cd32d937/train.h5
2022-02-10 13:47:48,943 P36078 INFO Loading data from h5: ../data/Movielens/movielenslatest_x1_cd32d937/valid.h5
2022-02-10 13:47:48,976 P36078 INFO Train samples: total/1404801, pos/467878, neg/936923, ratio/33.31%, blocks/1
2022-02-10 13:47:48,977 P36078 INFO Validation samples: total/401372, pos/134225, neg/267147, ratio/33.44%, blocks/1
2022-02-10 13:47:48,978 P36078 INFO Loading train data done.
2022-02-10 13:48:03,796 P36078 INFO Total number of parameters: 1238542.
2022-02-10 13:48:03,797 P36078 INFO Start training: 343 batches/epoch
2022-02-10 13:48:03,797 P36078 INFO ************ Epoch=1 start ************
2022-02-10 13:48:45,270 P36078 INFO [Metrics] AUC: 0.934311 - logloss: 0.292014
2022-02-10 13:48:45,281 P36078 INFO Save best model: monitor(max): 0.934311
2022-02-10 13:48:45,317 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:48:45,547 P36078 INFO Train loss: 0.379546
2022-02-10 13:48:45,547 P36078 INFO ************ Epoch=1 end ************
2022-02-10 13:49:30,804 P36078 INFO [Metrics] AUC: 0.944055 - logloss: 0.272700
2022-02-10 13:49:30,811 P36078 INFO Save best model: monitor(max): 0.944055
2022-02-10 13:49:30,852 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:49:31,077 P36078 INFO Train loss: 0.359097
2022-02-10 13:49:31,077 P36078 INFO ************ Epoch=2 end ************
2022-02-10 13:50:14,919 P36078 INFO [Metrics] AUC: 0.947627 - logloss: 0.257598
2022-02-10 13:50:14,920 P36078 INFO Save best model: monitor(max): 0.947627
2022-02-10 13:50:14,965 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:50:15,188 P36078 INFO Train loss: 0.360707
2022-02-10 13:50:15,188 P36078 INFO ************ Epoch=3 end ************
2022-02-10 13:50:56,866 P36078 INFO [Metrics] AUC: 0.949276 - logloss: 0.252871
2022-02-10 13:50:56,878 P36078 INFO Save best model: monitor(max): 0.949276
2022-02-10 13:50:56,957 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:50:57,243 P36078 INFO Train loss: 0.366489
2022-02-10 13:50:57,243 P36078 INFO ************ Epoch=4 end ************
2022-02-10 13:51:38,763 P36078 INFO [Metrics] AUC: 0.950254 - logloss: 0.249001
2022-02-10 13:51:38,765 P36078 INFO Save best model: monitor(max): 0.950254
2022-02-10 13:51:38,843 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:51:39,172 P36078 INFO Train loss: 0.370444
2022-02-10 13:51:39,172 P36078 INFO ************ Epoch=5 end ************
2022-02-10 13:52:21,032 P36078 INFO [Metrics] AUC: 0.951529 - logloss: 0.246459
2022-02-10 13:52:21,042 P36078 INFO Save best model: monitor(max): 0.951529
2022-02-10 13:52:21,097 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:52:21,301 P36078 INFO Train loss: 0.374334
2022-02-10 13:52:21,301 P36078 INFO ************ Epoch=6 end ************
2022-02-10 13:53:03,340 P36078 INFO [Metrics] AUC: 0.953046 - logloss: 0.242244
2022-02-10 13:53:03,345 P36078 INFO Save best model: monitor(max): 0.953046
2022-02-10 13:53:03,363 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:53:03,661 P36078 INFO Train loss: 0.375143
2022-02-10 13:53:03,661 P36078 INFO ************ Epoch=7 end ************
2022-02-10 13:53:47,573 P36078 INFO [Metrics] AUC: 0.953973 - logloss: 0.240622
2022-02-10 13:53:47,579 P36078 INFO Save best model: monitor(max): 0.953973
2022-02-10 13:53:47,604 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:53:47,779 P36078 INFO Train loss: 0.377144
2022-02-10 13:53:47,780 P36078 INFO ************ Epoch=8 end ************
2022-02-10 13:54:29,505 P36078 INFO [Metrics] AUC: 0.954090 - logloss: 0.238773
2022-02-10 13:54:29,509 P36078 INFO Save best model: monitor(max): 0.954090
2022-02-10 13:54:29,533 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:54:29,814 P36078 INFO Train loss: 0.375621
2022-02-10 13:54:29,814 P36078 INFO ************ Epoch=9 end ************
2022-02-10 13:55:08,082 P36078 INFO [Metrics] AUC: 0.955372 - logloss: 0.235571
2022-02-10 13:55:08,083 P36078 INFO Save best model: monitor(max): 0.955372
2022-02-10 13:55:08,115 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:55:08,368 P36078 INFO Train loss: 0.376009
2022-02-10 13:55:08,368 P36078 INFO ************ Epoch=10 end ************
2022-02-10 13:55:46,247 P36078 INFO [Metrics] AUC: 0.955174 - logloss: 0.236176
2022-02-10 13:55:46,254 P36078 INFO Monitor(max) STOP: 0.955174 !
2022-02-10 13:55:46,254 P36078 INFO Reduce learning rate on plateau: 0.000100
2022-02-10 13:55:46,254 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:55:46,650 P36078 INFO Train loss: 0.376239
2022-02-10 13:55:46,650 P36078 INFO ************ Epoch=11 end ************
2022-02-10 13:56:27,778 P36078 INFO [Metrics] AUC: 0.967495 - logloss: 0.205305
2022-02-10 13:56:27,779 P36078 INFO Save best model: monitor(max): 0.967495
2022-02-10 13:56:27,889 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:56:28,203 P36078 INFO Train loss: 0.278775
2022-02-10 13:56:28,203 P36078 INFO ************ Epoch=12 end ************
2022-02-10 13:57:08,389 P36078 INFO [Metrics] AUC: 0.969260 - logloss: 0.209989
2022-02-10 13:57:08,396 P36078 INFO Save best model: monitor(max): 0.969260
2022-02-10 13:57:08,483 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:57:08,755 P36078 INFO Train loss: 0.193920
2022-02-10 13:57:08,755 P36078 INFO ************ Epoch=13 end ************
2022-02-10 13:57:51,130 P36078 INFO [Metrics] AUC: 0.968248 - logloss: 0.230470
2022-02-10 13:57:51,143 P36078 INFO Monitor(max) STOP: 0.968248 !
2022-02-10 13:57:51,144 P36078 INFO Reduce learning rate on plateau: 0.000010
2022-02-10 13:57:51,144 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:57:51,446 P36078 INFO Train loss: 0.150512
2022-02-10 13:57:51,447 P36078 INFO ************ Epoch=14 end ************
2022-02-10 13:58:29,384 P36078 INFO [Metrics] AUC: 0.967887 - logloss: 0.244538
2022-02-10 13:58:29,387 P36078 INFO Monitor(max) STOP: 0.967887 !
2022-02-10 13:58:29,389 P36078 INFO Reduce learning rate on plateau: 0.000001
2022-02-10 13:58:29,389 P36078 INFO Early stopping at epoch=15
2022-02-10 13:58:29,391 P36078 INFO --- 343/343 batches finished ---
2022-02-10 13:58:29,619 P36078 INFO Train loss: 0.117196
2022-02-10 13:58:29,619 P36078 INFO Training finished.
2022-02-10 13:58:29,620 P36078 INFO Load best model: /home/XXX/benchmarks/Movielens/DeepIM_movielenslatest_x1/movielenslatest_x1_cd32d937/DeepIM_movielenslatest_x1_001_eb1c9e99.model
2022-02-10 13:58:29,634 P36078 INFO ****** Validation evaluation ******
2022-02-10 13:58:38,085 P36078 INFO [Metrics] AUC: 0.969260 - logloss: 0.209989
2022-02-10 13:58:38,373 P36078 INFO ******** Test evaluation ********
2022-02-10 13:58:38,378 P36078 INFO Loading data...
2022-02-10 13:58:38,413 P36078 INFO Loading data from h5: ../data/Movielens/movielenslatest_x1_cd32d937/test.h5
2022-02-10 13:58:38,430 P36078 INFO Test samples: total/200686, pos/66850, neg/133836, ratio/33.31%, blocks/1
2022-02-10 13:58:38,431 P36078 INFO Loading test data done.
2022-02-10 13:58:41,787 P36078 INFO [Metrics] AUC: 0.969316 - logloss: 0.209861

```
