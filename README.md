# Enhanced-Federated-Averaging

To run the code, 
First install these libraires
   - torchvision==0.8.1+cu110
   - numpy==1.19.4
   - torch==1.7.0+cu110

# How to use
- step1 - download the provided folder
- step2 - Go to the root directory of main.py file
- step3. Now to get the results run the following scripts in the terminal of any IDE such as PyCharm, VsCode or Spyder
  For FashionMNIST
  1. wait-minibatch
```
python3 main.py -data fashion -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.1 -lr-global 1.0 -wait-all 1 -full-batch 0 -out fashion_wait_minibatch.csv
```
  2. wait-full
```
python3 main.py -data fashion -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.1 -lr-global 1.0 -wait-all 1 -full-batch 1 -out fashion_wait_full.csv
```
  4. algo1 without amplification
```
python3 main.py -data fashion -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.00001 -lr-global 1.0 -out fashion_alg1_no_amplify.csv
```
  6. algo1. with amplification
```
python3 main.py -data fashion -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.00001 -lr-global 10.0 -out fashion_alg1_amplify.csv
```
  
  
  
  For GTSRB
  1. wait-minibatch
```
python3 main.py -data gtsrb -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.1 -lr-global 1.0 -wait-all 1 -full-batch 0 -out gtsrb_wait_minibatch.csv
```
  3. wait-full
```
python3 main.py -data gtsrb -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.1 -lr-global 1.0 -wait-all 1 -full-batch 1 -out gtsrb_wait_full.csv
```
  4. algo1 without amplification
```
  python3 main.py -data gtsrb -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.00001 -lr-global 1.0 -out gtsrb_alg1_no_amplify.csv
```
  5. algo1. with amplification
```
python3 main.py -data gtsrb -availability periodic -seeds 1 -lr-warmup 0.1 -iters-warmup 10000 -iters-total 1500000 -lr 0.00001 -lr-global 10.0 -out gtsrb_alg1_amplify.csv
```


Results will be saved in the csv files named in the scripts (after the -out)

Flow of the Code
```
- dataset
  |-- __init__.py
  |-- dataset.py      : This file contains the code for downloading the datasets in the required formats
- model
  |-- __init__.py
  |-- cnn_cifar10.py  : This file contains the code for CNN model created for cifar dataset
  |-- cnn_mnist.py    :  This file contains the code for CNN model created for FashionMNIST dataset
  |-- cnn_gtsrb.py    : This file contains the code for CNN model created for GTSRB dataset
  |-- model.py
- Results_FashionMNIST: This folder contains the results obtained by me on FashionMNIST dataset
- Results_GTSRB       : This folder contains the results obtained by me on GTSRB dataset
- statistic
  |-- __init__.py
  |-- collect_stat.py : This file contains the code for writing the results in .csv file
- util
  |-- __init__.py
  |-- util.py         : This file contains the code for splitting the dataset among the clients
- config.py         : This file contains the code for capturing the arguiments provided in the python script in terminal
- main.py           : This file contain the code of algoritm proposed by authors
```
When running the script, first .config file is executed which collect the arguments and then select the call the dataset.py file to download the requred
data, then it splits the data among clients by calling the utils.py file. Then it select the corresponding CNN model for the dataset.
collect_stat.py file initialize the .csv file for writing the results for federated learning rounds.
Finally .main file is executed which have code for implementation of the proposed algorithm.
