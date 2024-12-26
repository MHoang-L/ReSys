# Project Overview: News Recommendation Challenge on MIND Dataset

**Models and Dataset**

| Full name                                                                 | Paper                                              | Summary
| ------------------------------------------------------------------------- |:--------------------------------------------------:|:-------------------------------------:|
| Neural News Recommendation with Multi-Head Self-Attention                 | [NRMS](https://aclanthology.org/D19-1671.pdf)         | [NRMS](https://github.com/ducdinhchu/MIND-news-recommendation/blob/master/S_NRMS.pdf)
| Fastformer: Additive Attention Can Be All You Need                        | [Fastformer](https://arxiv.org/pdf/2108.09084.pdf) | [Fastformer](https://github.com/ducdinhchu/MIND-news-recommendation/blob/master/S_Fastformer.pdf)
| MIND: A Large-scale Dataset for News Recommendation                       | [MIND](https://aclanthology.org/2020.acl-main.331.pdf)     | [MIND](https://github.com/ducdinhchu/MIND-news-recommendation/blob/master/S_MIND.pdf)

**Results**

| Rank | User          | Entries | Date of Last Entry | AUC     | MRR    | nDCG@5  | nDCG@10 |
|:----:|:-------------:|:-------:|:------------------:|:-------:|:------:|:-------:|:-------:|
|  28  | martinmarshall|    3    |      12/26/24      | 0.7042  | 0.3561 | 0.3901  | 0.4462  |

## Environment
Please follow the setup steps bellow:
1. Install [Anaconda](https://www.anaconda.com/products/distribution)
2. Create a virtual environment by using conda command 
```
$> conda env create -n deepnewsrec python=3.11.3
```
3. Activate the virtual environment we created
```commandline
$> conda activate deepnewsrec
```
4. Install mlflow
```commandline
(deepnewsrec)$> pip install mlflow==1.29.0
```

## How to run the code
- Try a toy example with `demo` dataset 
```commandline 
$> mlflow run -e train --env-manager=local --experiment-name individual_runs -P mind_type=large -P epochs=1 -P batch_size=32 .
mlflow run -e train --no-conda --experiment-name individual_runs -P mind_type=large -P model_type=nrms -P epochs=10 -P batch_size=32 .
```
or you can use git uri
```commandline
$> mlflow run -e train --experiment-name individual_runs -P mind_type=demo -P epochs=1 git@github.com:hongjunyan/pytorch-news-recommendation.git 
```

- Run hyperparameter tuning
```commandline
$> mlflow run -e tune_with_ray --experiment-name tune_hyperparams -P mind_type=demo -P epochs=1 .
```
For training a formal model, please use `mind_type=large`.

## Prediction
Run prediction using saved checkpoint:
```
python submission.py `
--pretrained_model_path ./saved_ckpt `
--pretreained_model others `
--root_data_dir ./data/speedy_data/ `
--num_hidden_layers 8 `
--load_ckpt_name ./saved_ckpt/saved_model.pt `
--batch_size 256 
```
It will creates a zip file:`predciton.zip`, which can be submitted to the leaderboard of MIND directly.  
