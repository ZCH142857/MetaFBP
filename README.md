# Setup
## Runtime

The main python libraries we use:
- Python 3.8
- torch 1.8.1
- numpy 1.19.2

## Datasets
Please download these following datasets and unzip into `datasets`:

Download link:  [THU_Cloud](https://cloud.tsinghua.edu.cn/f/b5f39ae98736445798ac/?dl=1)

You can also change the root directory of datasets by modifying the default value of the argument `--data-root` in [train_fea.py](train_fea.py), [train.py](train.py), and [test.py](test.py):
```python
    # train_fea.py
    parser.add_argument('--data-root', type=str, default='./datasets')
    # train.py
    parser.add_argument('--data-root', type=str, default='./datasets')
    # test.py
    parser.add_argument('--data-root', type=str, default='./datasets')
```

## Results

Download link:  [THU_Cloud](https://cloud.tsinghua.edu.cn/f/e1e06ec4a2614fedbb3a/?dl=1)

# Run
The directory structure of code may like this:
```text
MetaFBP/
    |–– data/
    |–– datasets/
        |–– FBP5500/
        |–– FBPSCUT/
        |–– US10K/
    |–– model/
    |–– util/
    README.md
    test.py
    test_fea.py
    train.py
    train.sh
    train_fea.py
    train_fea.sh
```
1. Train the universal feature extractor for each dataset:
    ```shell
    bash train_fea.sh PFBP-SCUT5500
    bash train_fea.sh PFBP-SCUT500
    bash train_fea.sh PFBP-US10K
    ```
    Usage of `train_fea.sh`:
    ```text
    bash train_fea.sh {arg1=dataset}
    ```
    - `dataset` specifies which dataset to train on, available ones are: `PFBP-SCUT5500`,`PFBP-SCUT500`, `PFBP-US10K`

2. Once the universal feature extractor is ready, you can run the experiments of PFBP task. For example, the following cmd runs the experiment of `MetaFBP-R` on PFBP-SCUT5500 benchmark with 5-way K-shot regression:
    ```shell
    bash train.sh MetaFBP-R PFBP-SCUT5500
    ```
    Usage of `train.sh`:
    ```text
    bash train.sh {arg1=model} {arg2=dataset}
    ```
    - `model` specifies which model to use, available ones are: `Base-MAML`,`MetaFBP-R`, `MetaFBP-T`
    - `dataset` specifies which dataset to train and test on, available ones are: `PFBP-SCUT5500`,`PFBP-SCUT500`, `PFBP-US10K`
