## AutoInt+_criteo_x1

A hands-on guide to run the AutoInt model on the Criteo_x1 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) Gold 6278C CPU @ 2.60GHz
  GPU: Tesla V100 32G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 10.2
  python: 3.6.4
  pytorch: 1.0.0
  pandas: 0.22.0
  numpy: 1.19.2
  scipy: 1.5.4
  sklearn: 0.22.1
  pyyaml: 5.4.1
  h5py: 2.8.0
  tqdm: 4.60.0
  fuxictr: 1.1.0

  ```

### Dataset
Dataset ID: [Criteo_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Criteo/README.md#Criteo_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/tree/v1.1.0) for this experiment. See the model code: [AutoInt](https://github.com/xue-pai/FuxiCTR/blob/v1.1.0/fuxictr/pytorch/models/AutoInt.py).

Running steps:

1. Download [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.0.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Criteo/Criteo_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [AutoInt+_criteo_x1_tuner_config_03](./AutoInt+_criteo_x1_tuner_config_03). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd AutoInt+_criteo_x1
    nohup python run_expid.py --config ./AutoInt+_criteo_x1_tuner_config_03 --expid AutoInt_criteo_x1_013_cb9a6c60 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

Total 5 runs:

| Runs | AUC | logloss  |
|:--------------------:|:--------------------:|:--------------------:|
| 1 | 0.813996 | 0.438018  |
| 2 | 0.813945 | 0.438009  |
| 3 | 0.813806 | 0.438117  |
| 4 | 0.814035 | 0.437933  |
| 5 | 0.813662 | 0.438200  |
| Avg | 0.813889 | 0.438055 |
| Std | &#177;0.00013735 | &#177;0.00009299 |


### Logs
```python
2022-01-23 16:08:10,060 P845 INFO {
    "attention_dim": "128",
    "attention_layers": "3",
    "batch_norm": "True",
    "batch_size": "4096",
    "data_block_size": "-1",
    "data_format": "csv",
    "data_root": "../data/Criteo/",
    "dataset_id": "criteo_x1_7b681156",
    "debug": "False",
    "dnn_activations": "relu",
    "dnn_hidden_units": "[400, 400, 400]",
    "embedding_dim": "10",
    "embedding_regularizer": "1e-05",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['I1', 'I2', 'I3', 'I4', 'I5', 'I6', 'I7', 'I8', 'I9', 'I10', 'I11', 'I12', 'I13'], 'type': 'numeric'}, {'active': True, 'dtype': 'float', 'name': ['C1', 'C2', 'C3', 'C4', 'C5', 'C6', 'C7', 'C8', 'C9', 'C10', 'C11', 'C12', 'C13', 'C14', 'C15', 'C16', 'C17', 'C18', 'C19', 'C20', 'C21', 'C22', 'C23', 'C24', 'C25', 'C26'], 'type': 'categorical'}]",
    "gpu": "4",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "layer_norm": "False",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "AutoInt",
    "model_id": "AutoInt_criteo_x1_013_cb9a6c60",
    "model_root": "./Criteo/AutoInt_criteo_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0.1",
    "net_regularizer": "0",
    "num_heads": "1",
    "num_workers": "3",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Criteo/Criteo_x1/test.csv",
    "train_data": "../data/Criteo/Criteo_x1/train.csv",
    "use_hdf5": "True",
    "use_residual": "True",
    "use_scale": "False",
    "use_wide": "True",
    "valid_data": "../data/Criteo/Criteo_x1/valid.csv",
    "verbose": "0",
    "version": "pytorch"
}
2022-01-23 16:08:10,060 P845 INFO Set up feature encoder...
2022-01-23 16:08:10,060 P845 INFO Load feature_map from json: ../data/Criteo/criteo_x1_7b681156/feature_map.json
2022-01-23 16:08:10,061 P845 INFO Loading data...
2022-01-23 16:08:10,061 P845 INFO Loading data from h5: ../data/Criteo/criteo_x1_7b681156/train.h5
2022-01-23 16:08:14,827 P845 INFO Loading data from h5: ../data/Criteo/criteo_x1_7b681156/valid.h5
2022-01-23 16:08:16,004 P845 INFO Train samples: total/33003326, pos/8456369, neg/24546957, ratio/25.62%, blocks/1
2022-01-23 16:08:16,004 P845 INFO Validation samples: total/8250124, pos/2114300, neg/6135824, ratio/25.63%, blocks/1
2022-01-23 16:08:16,004 P845 INFO Loading train data done.
2022-01-23 16:08:25,261 P845 INFO Total number of parameters: 23537894.
2022-01-23 16:08:25,261 P845 INFO Start training: 8058 batches/epoch
2022-01-23 16:08:25,261 P845 INFO ************ Epoch=1 start ************
2022-01-23 17:02:33,083 P845 INFO [Metrics] AUC: 0.803284 - logloss: 0.448011
2022-01-23 17:02:33,084 P845 INFO Save best model: monitor(max): 0.803284
2022-01-23 17:02:33,378 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 17:02:33,414 P845 INFO Train loss: 0.462635
2022-01-23 17:02:33,414 P845 INFO ************ Epoch=1 end ************
2022-01-23 17:56:35,555 P845 INFO [Metrics] AUC: 0.805767 - logloss: 0.445510
2022-01-23 17:56:35,556 P845 INFO Save best model: monitor(max): 0.805767
2022-01-23 17:56:35,658 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 17:56:35,703 P845 INFO Train loss: 0.457614
2022-01-23 17:56:35,703 P845 INFO ************ Epoch=2 end ************
2022-01-23 18:50:43,277 P845 INFO [Metrics] AUC: 0.806940 - logloss: 0.444555
2022-01-23 18:50:43,278 P845 INFO Save best model: monitor(max): 0.806940
2022-01-23 18:50:43,385 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 18:50:43,424 P845 INFO Train loss: 0.456462
2022-01-23 18:50:43,424 P845 INFO ************ Epoch=3 end ************
2022-01-23 19:44:57,590 P845 INFO [Metrics] AUC: 0.807686 - logloss: 0.443884
2022-01-23 19:44:57,591 P845 INFO Save best model: monitor(max): 0.807686
2022-01-23 19:44:57,702 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 19:44:57,747 P845 INFO Train loss: 0.456894
2022-01-23 19:44:57,748 P845 INFO ************ Epoch=4 end ************
2022-01-23 20:39:16,060 P845 INFO [Metrics] AUC: 0.808087 - logloss: 0.443520
2022-01-23 20:39:16,061 P845 INFO Save best model: monitor(max): 0.808087
2022-01-23 20:39:16,192 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 20:39:16,231 P845 INFO Train loss: 0.459197
2022-01-23 20:39:16,231 P845 INFO ************ Epoch=5 end ************
2022-01-23 21:33:36,769 P845 INFO [Metrics] AUC: 0.808468 - logloss: 0.443044
2022-01-23 21:33:36,771 P845 INFO Save best model: monitor(max): 0.808468
2022-01-23 21:33:36,876 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 21:33:36,920 P845 INFO Train loss: 0.463282
2022-01-23 21:33:36,920 P845 INFO ************ Epoch=6 end ************
2022-01-23 22:28:02,305 P845 INFO [Metrics] AUC: 0.808623 - logloss: 0.442921
2022-01-23 22:28:02,306 P845 INFO Save best model: monitor(max): 0.808623
2022-01-23 22:28:02,416 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 22:28:02,458 P845 INFO Train loss: 0.466389
2022-01-23 22:28:02,458 P845 INFO ************ Epoch=7 end ************
2022-01-23 23:22:24,809 P845 INFO [Metrics] AUC: 0.808936 - logloss: 0.442736
2022-01-23 23:22:24,811 P845 INFO Save best model: monitor(max): 0.808936
2022-01-23 23:22:24,910 P845 INFO --- 8058/8058 batches finished ---
2022-01-23 23:22:24,955 P845 INFO Train loss: 0.466420
2022-01-23 23:22:24,955 P845 INFO ************ Epoch=8 end ************
2022-01-24 00:16:45,419 P845 INFO [Metrics] AUC: 0.809023 - logloss: 0.442552
2022-01-24 00:16:45,420 P845 INFO Save best model: monitor(max): 0.809023
2022-01-24 00:16:45,534 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 00:16:45,574 P845 INFO Train loss: 0.465934
2022-01-24 00:16:45,574 P845 INFO ************ Epoch=9 end ************
2022-01-24 01:11:06,900 P845 INFO [Metrics] AUC: 0.809281 - logloss: 0.442364
2022-01-24 01:11:06,901 P845 INFO Save best model: monitor(max): 0.809281
2022-01-24 01:11:07,003 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 01:11:07,042 P845 INFO Train loss: 0.465963
2022-01-24 01:11:07,042 P845 INFO ************ Epoch=10 end ************
2022-01-24 02:05:08,401 P845 INFO [Metrics] AUC: 0.809329 - logloss: 0.442293
2022-01-24 02:05:08,403 P845 INFO Save best model: monitor(max): 0.809329
2022-01-24 02:05:08,507 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 02:05:08,549 P845 INFO Train loss: 0.466080
2022-01-24 02:05:08,549 P845 INFO ************ Epoch=11 end ************
2022-01-24 02:59:22,965 P845 INFO [Metrics] AUC: 0.809419 - logloss: 0.442168
2022-01-24 02:59:22,966 P845 INFO Save best model: monitor(max): 0.809419
2022-01-24 02:59:23,082 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 02:59:23,128 P845 INFO Train loss: 0.466046
2022-01-24 02:59:23,128 P845 INFO ************ Epoch=12 end ************
2022-01-24 03:53:36,309 P845 INFO [Metrics] AUC: 0.809504 - logloss: 0.442149
2022-01-24 03:53:36,310 P845 INFO Save best model: monitor(max): 0.809504
2022-01-24 03:53:36,427 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 03:53:36,473 P845 INFO Train loss: 0.465928
2022-01-24 03:53:36,473 P845 INFO ************ Epoch=13 end ************
2022-01-24 04:31:29,156 P845 INFO [Metrics] AUC: 0.809497 - logloss: 0.442190
2022-01-24 04:31:29,158 P845 INFO Monitor(max) STOP: 0.809497 !
2022-01-24 04:31:29,158 P845 INFO Reduce learning rate on plateau: 0.000100
2022-01-24 04:31:29,158 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 04:31:29,200 P845 INFO Train loss: 0.466300
2022-01-24 04:31:29,200 P845 INFO ************ Epoch=14 end ************
2022-01-24 05:07:54,681 P845 INFO [Metrics] AUC: 0.813147 - logloss: 0.438843
2022-01-24 05:07:54,683 P845 INFO Save best model: monitor(max): 0.813147
2022-01-24 05:07:54,788 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 05:07:54,835 P845 INFO Train loss: 0.446756
2022-01-24 05:07:54,835 P845 INFO ************ Epoch=15 end ************
2022-01-24 05:44:19,297 P845 INFO [Metrics] AUC: 0.813549 - logloss: 0.438513
2022-01-24 05:44:19,299 P845 INFO Save best model: monitor(max): 0.813549
2022-01-24 05:44:19,415 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 05:44:19,454 P845 INFO Train loss: 0.437118
2022-01-24 05:44:19,454 P845 INFO ************ Epoch=16 end ************
2022-01-24 06:20:38,126 P845 INFO [Metrics] AUC: 0.813568 - logloss: 0.438538
2022-01-24 06:20:38,128 P845 INFO Save best model: monitor(max): 0.813568
2022-01-24 06:20:38,227 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 06:20:38,274 P845 INFO Train loss: 0.434781
2022-01-24 06:20:38,274 P845 INFO ************ Epoch=17 end ************
2022-01-24 06:57:01,250 P845 INFO [Metrics] AUC: 0.813351 - logloss: 0.438794
2022-01-24 06:57:01,252 P845 INFO Monitor(max) STOP: 0.813351 !
2022-01-24 06:57:01,253 P845 INFO Reduce learning rate on plateau: 0.000010
2022-01-24 06:57:01,253 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 06:57:01,291 P845 INFO Train loss: 0.433349
2022-01-24 06:57:01,291 P845 INFO ************ Epoch=18 end ************
2022-01-24 07:33:28,932 P845 INFO [Metrics] AUC: 0.810665 - logloss: 0.442605
2022-01-24 07:33:28,933 P845 INFO Monitor(max) STOP: 0.810665 !
2022-01-24 07:33:28,933 P845 INFO Reduce learning rate on plateau: 0.000001
2022-01-24 07:33:28,933 P845 INFO Early stopping at epoch=19
2022-01-24 07:33:28,933 P845 INFO --- 8058/8058 batches finished ---
2022-01-24 07:33:28,973 P845 INFO Train loss: 0.426588
2022-01-24 07:33:28,973 P845 INFO Training finished.
2022-01-24 07:33:28,973 P845 INFO Load best model: /cache/FuxiCTR/benchmarks/Criteo/AutoInt_criteo_x1/criteo_x1_7b681156/AutoInt_criteo_x1_013_cb9a6c60.model
2022-01-24 07:33:32,207 P845 INFO ****** Validation evaluation ******
2022-01-24 07:34:31,055 P845 INFO [Metrics] AUC: 0.813568 - logloss: 0.438538
2022-01-24 07:34:31,138 P845 INFO ******** Test evaluation ********
2022-01-24 07:34:31,138 P845 INFO Loading data...
2022-01-24 07:34:31,138 P845 INFO Loading data from h5: ../data/Criteo/criteo_x1_7b681156/test.h5
2022-01-24 07:34:31,892 P845 INFO Test samples: total/4587167, pos/1174769, neg/3412398, ratio/25.61%, blocks/1
2022-01-24 07:34:31,892 P845 INFO Loading test data done.
2022-01-24 07:35:04,050 P845 INFO [Metrics] AUC: 0.813996 - logloss: 0.438018

```
