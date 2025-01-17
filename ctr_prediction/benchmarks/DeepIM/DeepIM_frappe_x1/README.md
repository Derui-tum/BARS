## DeepIM_frappe_x1

A hands-on guide to run the DeepIM model on the Frappe_x1 dataset.

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
Dataset ID: [Frappe_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Frappe/README.md#Frappe_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/tree/v1.1.0) for this experiment. See the model code: [DeepIM](https://github.com/xue-pai/FuxiCTR/blob/v1.1.0/fuxictr/pytorch/models/DeepIM.py).

Running steps:

1. Download [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.0.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Frappe/Frappe_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [DeepIM_frappe_x1_tuner_config_01](./DeepIM_frappe_x1_tuner_config_01). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd DeepIM_frappe_x1
    nohup python run_expid.py --config ./DeepIM_frappe_x1_tuner_config_01 --expid DeepIM_frappe_x1_001_a11ff117 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

Total 5 runs:

| Runs | AUC | logloss  |
|:--------------------:|:--------------------:|:--------------------:|
| 1 | 0.984448 | 0.149010  |
| 2 | 0.983098 | 0.152701  |
| 3 | 0.984255 | 0.142934  |
| 4 | 0.982874 | 0.158292  |
| 5 | 0.983420 | 0.145777  |
| Avg | 0.983619 | 0.149743 |
| Std | &#177;0.00062575 | &#177;0.00537520 |


### Logs
```python
2022-02-10 13:27:07,503 P33359 INFO {
    "batch_size": "4096",
    "data_format": "csv",
    "data_root": "../data/Frappe/",
    "dataset_id": "frappe_x1_04e961e9",
    "debug": "False",
    "embedding_dim": "10",
    "embedding_regularizer": "0.05",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['user', 'item', 'daytime', 'weekday', 'isweekend', 'homework', 'cost', 'weather', 'country', 'city'], 'type': 'categorical'}]",
    "gpu": "0",
    "hidden_activations": "relu",
    "hidden_units": "[400, 400, 400]",
    "im_batch_norm": "False",
    "im_order": "3",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "DeepIM",
    "model_id": "DeepIM_frappe_x1_001_a11ff117",
    "model_root": "./Frappe/DeepIM_frappe_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_batch_norm": "True",
    "net_dropout": "0.1",
    "net_regularizer": "0",
    "num_workers": "3",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Frappe/Frappe_x1/test.csv",
    "train_data": "../data/Frappe/Frappe_x1/train.csv",
    "use_hdf5": "True",
    "valid_data": "../data/Frappe/Frappe_x1/valid.csv",
    "verbose": "1",
    "version": "pytorch"
}
2022-02-10 13:27:07,504 P33359 INFO Set up feature encoder...
2022-02-10 13:27:07,505 P33359 INFO Load feature_map from json: ../data/Frappe/frappe_x1_04e961e9/feature_map.json
2022-02-10 13:27:07,505 P33359 INFO Loading data...
2022-02-10 13:27:07,509 P33359 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/train.h5
2022-02-10 13:27:07,559 P33359 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/valid.h5
2022-02-10 13:27:07,583 P33359 INFO Train samples: total/202027, pos/67604, neg/134423, ratio/33.46%, blocks/1
2022-02-10 13:27:07,583 P33359 INFO Validation samples: total/57722, pos/19063, neg/38659, ratio/33.03%, blocks/1
2022-02-10 13:27:07,584 P33359 INFO Loading train data done.
2022-02-10 13:27:28,714 P33359 INFO Total number of parameters: 417922.
2022-02-10 13:27:28,715 P33359 INFO Start training: 50 batches/epoch
2022-02-10 13:27:28,715 P33359 INFO ************ Epoch=1 start ************
2022-02-10 13:27:38,054 P33359 INFO [Metrics] AUC: 0.936303 - logloss: 0.672567
2022-02-10 13:27:38,054 P33359 INFO Save best model: monitor(max): 0.936303
2022-02-10 13:27:38,080 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:27:38,289 P33359 INFO Train loss: 0.355558
2022-02-10 13:27:38,290 P33359 INFO ************ Epoch=1 end ************
2022-02-10 13:27:47,568 P33359 INFO [Metrics] AUC: 0.964309 - logloss: 0.239890
2022-02-10 13:27:47,583 P33359 INFO Save best model: monitor(max): 0.964309
2022-02-10 13:27:47,604 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:27:47,783 P33359 INFO Train loss: 0.265729
2022-02-10 13:27:47,783 P33359 INFO ************ Epoch=2 end ************
2022-02-10 13:27:55,444 P33359 INFO [Metrics] AUC: 0.975334 - logloss: 0.183212
2022-02-10 13:27:55,445 P33359 INFO Save best model: monitor(max): 0.975334
2022-02-10 13:27:55,469 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:27:55,625 P33359 INFO Train loss: 0.216922
2022-02-10 13:27:55,626 P33359 INFO ************ Epoch=3 end ************
2022-02-10 13:28:04,713 P33359 INFO [Metrics] AUC: 0.977162 - logloss: 0.183473
2022-02-10 13:28:04,713 P33359 INFO Save best model: monitor(max): 0.977162
2022-02-10 13:28:04,741 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:28:04,955 P33359 INFO Train loss: 0.191610
2022-02-10 13:28:04,955 P33359 INFO ************ Epoch=4 end ************
2022-02-10 13:28:14,648 P33359 INFO [Metrics] AUC: 0.978407 - logloss: 0.168452
2022-02-10 13:28:14,659 P33359 INFO Save best model: monitor(max): 0.978407
2022-02-10 13:28:14,682 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:28:14,844 P33359 INFO Train loss: 0.180325
2022-02-10 13:28:14,844 P33359 INFO ************ Epoch=5 end ************
2022-02-10 13:28:24,595 P33359 INFO [Metrics] AUC: 0.979042 - logloss: 0.208605
2022-02-10 13:28:24,599 P33359 INFO Save best model: monitor(max): 0.979042
2022-02-10 13:28:24,616 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:28:24,783 P33359 INFO Train loss: 0.176669
2022-02-10 13:28:24,783 P33359 INFO ************ Epoch=6 end ************
2022-02-10 13:28:34,640 P33359 INFO [Metrics] AUC: 0.980296 - logloss: 0.162306
2022-02-10 13:28:34,640 P33359 INFO Save best model: monitor(max): 0.980296
2022-02-10 13:28:34,669 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:28:34,861 P33359 INFO Train loss: 0.168830
2022-02-10 13:28:34,862 P33359 INFO ************ Epoch=7 end ************
2022-02-10 13:28:43,116 P33359 INFO [Metrics] AUC: 0.980675 - logloss: 0.180564
2022-02-10 13:28:43,123 P33359 INFO Save best model: monitor(max): 0.980675
2022-02-10 13:28:43,131 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:28:43,327 P33359 INFO Train loss: 0.168186
2022-02-10 13:28:43,328 P33359 INFO ************ Epoch=8 end ************
2022-02-10 13:28:52,208 P33359 INFO [Metrics] AUC: 0.981857 - logloss: 0.154874
2022-02-10 13:28:52,209 P33359 INFO Save best model: monitor(max): 0.981857
2022-02-10 13:28:52,231 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:28:52,528 P33359 INFO Train loss: 0.163475
2022-02-10 13:28:52,529 P33359 INFO ************ Epoch=9 end ************
2022-02-10 13:29:02,420 P33359 INFO [Metrics] AUC: 0.981827 - logloss: 0.158594
2022-02-10 13:29:02,432 P33359 INFO Monitor(max) STOP: 0.981827 !
2022-02-10 13:29:02,433 P33359 INFO Reduce learning rate on plateau: 0.000100
2022-02-10 13:29:02,433 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:29:02,615 P33359 INFO Train loss: 0.162784
2022-02-10 13:29:02,615 P33359 INFO ************ Epoch=10 end ************
2022-02-10 13:29:12,570 P33359 INFO [Metrics] AUC: 0.984017 - logloss: 0.145236
2022-02-10 13:29:12,606 P33359 INFO Save best model: monitor(max): 0.984017
2022-02-10 13:29:12,616 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:29:12,831 P33359 INFO Train loss: 0.134405
2022-02-10 13:29:12,832 P33359 INFO ************ Epoch=11 end ************
2022-02-10 13:29:22,213 P33359 INFO [Metrics] AUC: 0.984650 - logloss: 0.142095
2022-02-10 13:29:22,218 P33359 INFO Save best model: monitor(max): 0.984650
2022-02-10 13:29:22,251 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:29:22,531 P33359 INFO Train loss: 0.112249
2022-02-10 13:29:22,531 P33359 INFO ************ Epoch=12 end ************
2022-02-10 13:29:30,798 P33359 INFO [Metrics] AUC: 0.984763 - logloss: 0.145687
2022-02-10 13:29:30,820 P33359 INFO Save best model: monitor(max): 0.984763
2022-02-10 13:29:30,847 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:29:31,034 P33359 INFO Train loss: 0.098448
2022-02-10 13:29:31,035 P33359 INFO ************ Epoch=13 end ************
2022-02-10 13:29:37,042 P33359 INFO [Metrics] AUC: 0.984863 - logloss: 0.147055
2022-02-10 13:29:37,050 P33359 INFO Save best model: monitor(max): 0.984863
2022-02-10 13:29:37,057 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:29:37,188 P33359 INFO Train loss: 0.089370
2022-02-10 13:29:37,189 P33359 INFO ************ Epoch=14 end ************
2022-02-10 13:29:43,456 P33359 INFO [Metrics] AUC: 0.984824 - logloss: 0.149619
2022-02-10 13:29:43,456 P33359 INFO Monitor(max) STOP: 0.984824 !
2022-02-10 13:29:43,462 P33359 INFO Reduce learning rate on plateau: 0.000010
2022-02-10 13:29:43,462 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:29:43,634 P33359 INFO Train loss: 0.081502
2022-02-10 13:29:43,634 P33359 INFO ************ Epoch=15 end ************
2022-02-10 13:29:51,615 P33359 INFO [Metrics] AUC: 0.984859 - logloss: 0.151014
2022-02-10 13:29:51,617 P33359 INFO Monitor(max) STOP: 0.984859 !
2022-02-10 13:29:51,618 P33359 INFO Reduce learning rate on plateau: 0.000001
2022-02-10 13:29:51,619 P33359 INFO Early stopping at epoch=16
2022-02-10 13:29:51,619 P33359 INFO --- 50/50 batches finished ---
2022-02-10 13:29:51,839 P33359 INFO Train loss: 0.075351
2022-02-10 13:29:51,839 P33359 INFO Training finished.
2022-02-10 13:29:51,839 P33359 INFO Load best model: /home/XXX/benchmarks/Frappe/DeepIM_frappe_x1/frappe_x1_04e961e9/DeepIM_frappe_x1_001_a11ff117.model
2022-02-10 13:29:51,851 P33359 INFO ****** Validation evaluation ******
2022-02-10 13:29:54,419 P33359 INFO [Metrics] AUC: 0.984863 - logloss: 0.147055
2022-02-10 13:29:54,681 P33359 INFO ******** Test evaluation ********
2022-02-10 13:29:54,682 P33359 INFO Loading data...
2022-02-10 13:29:54,682 P33359 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/test.h5
2022-02-10 13:29:54,704 P33359 INFO Test samples: total/28860, pos/9536, neg/19324, ratio/33.04%, blocks/1
2022-02-10 13:29:54,704 P33359 INFO Loading test data done.
2022-02-10 13:29:56,223 P33359 INFO [Metrics] AUC: 0.984448 - logloss: 0.149010

```
