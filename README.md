# AdaptiveReID: Adaptive L2 Regularization in Person Re-Identification

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/adaptivereid-adaptive-l2-regularization-in/person-re-identification-on-msmt17)](https://paperswithcode.com/sota/person-re-identification-on-msmt17?p=adaptivereid-adaptive-l2-regularization-in)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/adaptivereid-adaptive-l2-regularization-in/person-re-identification-on-market-1501)](https://paperswithcode.com/sota/person-re-identification-on-market-1501?p=adaptivereid-adaptive-l2-regularization-in)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/adaptivereid-adaptive-l2-regularization-in/person-re-identification-on-dukemtmc-reid)](https://paperswithcode.com/sota/person-re-identification-on-dukemtmc-reid?p=adaptivereid-adaptive-l2-regularization-in)

## Overview

We introduce an adaptive L2 regularization mechanism termed AdaptiveReID, in the setting of person re-identification.
In the literature, it is common practice to utilize hand-picked regularization factors which remain constant throughout the training procedure.
Unlike existing approaches, the regularization factors in our proposed method are updated adaptively through backpropagation.
This is achieved by incorporating trainable scalar variables as the regularization factors, which are further fed into a scaled hard sigmoid function.
Extensive experiments on the Market-1501, DukeMTMC-reID and MSMT17 datasets validate the effectiveness of our framework.
Most notably, we obtain state-of-the-art performance on MSMT17, which is the largest dataset for person re-identification.

## Environment

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
conda config --set auto_activate_base false
conda create --yes --name TensorFlow2.2 python=3.7
conda activate TensorFlow2.2
conda install --yes cudatoolkit=10.1 cudnn=7.6
conda install --yes cython matplotlib pandas pydot scikit-learn
pip install tensorflow==2.2.1
pip install opencv-python
pip install albumentations
```

## Training

```bash
python3 -u solution.py --dataset_name "Market1501" --backbone_model_name "ResNet50"
```

- To train on other datasets, replace `"Market1501"` with `"DukeMTMC_reID"` or `"MSMT17"`.
- To train with deeper backbones, replace `"ResNet50"` with `"ResNet101"` or `"ResNet152"`.
- To evaluate on a subset of the complete test set, append `--testing_size 0.5` to the command. Alternatively, you may turn this feature off by using `--testing_size 0.0`.

## Evaluation

```bash
python3 -u solution.py --dataset_name "Market1501" --backbone_model_name "ResNet50" --pretrained_model_file_path "?.h5" --output_folder_path "evaluation_only" --evaluation_only --freeze_backbone_for_N_epochs 0 --testing_size 1.0 --evaluate_testing_every_N_epochs 1
```

- Fill in the `pretrained_model_file_path` argument using the h5 file obtained during training.
- To use the re-ranking method, append `--use_re_ranking` to the command.
- You need to run this separate evaluation procedure only if `testing_size` is not set to `1.0` during training.

## Model Zoo

| Dataset | Backbone | mAP | Weights |
| - | - | - |- |
| Market1501 | ResNet50 | 88.3 | [Link](https://tuni-my.sharepoint.com/:u:/g/personal/xingyang_ni_tuni_fi/EbhPtp45rYFIlrOp4dfBUQEBY218NIYuXUTlax8SsqXqzA?e=x5CAFP) |
| DukeMTMC_reID | ResNet50 | 79.9 | [Link](https://tuni-my.sharepoint.com/:u:/g/personal/xingyang_ni_tuni_fi/EYinialkEvBFgc1mXpxRWWYBv7wHZzFCDmdM_4XR7k6tSA?e=Rpp3b7) |
| MSMT17 | ResNet50 | 59.4 | [Link](https://tuni-my.sharepoint.com/:u:/g/personal/xingyang_ni_tuni_fi/EWeswQHZdLlOhzfSCaJm2MsB9DCa3aYomZ-pDG4Ww7Uoyw?e=OueRHU) |
| MSMT17 | ResNet152 | 62.2 | [Link](https://tuni-my.sharepoint.com/:u:/g/personal/xingyang_ni_tuni_fi/EYrv4y--tXlOm9u4QJEX4uwB22oBtpJjoXPBr_Ry7xUbxg?e=GKdxyq) |

## Acknowledgements

- Evaluation Metrics are adapted from [deep-person-reid](https://github.com/KaiyangZhou/deep-person-reid/blob/v1.0.6/torchreid/metrics/rank_cylib/rank_cy.pyx).
- Re-Ranking is adapted from [person-re-ranking](https://github.com/zhunzhong07/person-re-ranking/blob/master/python-version/re_ranking_ranklist.py).
- Random Erasing is adapted from [Random-Erasing](https://github.com/zhunzhong07/Random-Erasing/blob/master/transforms.py).
- Triplet Loss is adapted from [triplet-reid](https://github.com/VisualComputingInstitute/triplet-reid/blob/master/loss.py).

## Citation

Please consider citing [AdaptiveReID](https://arxiv.org/abs/2007.07875) if it helps your research.

```
@article{ni2020adaptivereid,
  title={AdaptiveReID: Adaptive L2 Regularization in Person Re-Identification},
  author={Ni, Xingyang and Fang, Liang and Huttunen, Heikki},
  journal={arXiv preprint arXiv:2007.07875},
  year={2020}
}
```