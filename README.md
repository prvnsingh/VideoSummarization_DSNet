# DSNet: A Flexible Detect-to-Summarize Network for Video Summarization [[paper]](https://ieeexplore.ieee.org/document/9275314)

A PyTorch implementation of our paper [DSNet: A Flexible Detect-to-Summarize Network for Video Summarization](https://ieeexplore.ieee.org/document/9275314). Published in [IEEE Transactions on Image Processing](https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=83).

## Getting Started

This project is developed on Ubuntu 18.04 with CUDA 9.0.176.

Create a virtual environment with python 3.6, preferably using [Anaconda](https://www.anaconda.com/).

```sh
conda create --name dsnet python=3.6
conda activate dsnet
```

Install python dependencies.

```sh
pip install -r requirements.txt
```

## Datasets Preparation

Download the pre-processed datasets into `datasets/` folder, including [TVSum](https://github.com/yalesong/tvsum), [SumMe](https://gyglim.github.io/me/vsum/index.html) datasets.
downloading from any below links.

+ (Baidu Cloud) Link: https://pan.baidu.com/s/1LUK2aZzLvgNwbK07BUAQRQ Extraction Code: x09b
+ (Google Drive) https://drive.google.com/file/d/11ulsvk1MZI7iDqymw9cfL7csAYS0cDYH/view?usp=sharing

Now the datasets structure should look like

```
DSNet
└── datasets/
    ├── eccv16_dataset_ovp_google_pool5.h5
    ├── eccv16_dataset_summe_google_pool5.h5
    ├── eccv16_dataset_tvsum_google_pool5.h5
    ├── eccv16_dataset_youtube_google_pool5.h5
    └── readme.txt
```

## Training

### Anchor-free

Much similar to anchor-based models, to train on canonical TVSum and SumMe, run

```sh
python train.py anchor-free --model-dir ../models/af_basic --splits ../splits/tvsum.yml ../splits/summe.yml --nms-thresh 0.4
```

Note that NMS threshold is set to 0.4 for anchor-free models.

## Evaluation


For anchor-free models, remember to specify NMS threshold as 0.4.

```sh
python evaluate.py anchor-free --model-dir ../models/af_basic/ --splits ../splits/tvsum.yml ../splits/summe.yml --nms-thresh 0.4
```


### Inference

To predict the summary of a raw video, use `infer.py`. For example, run

```sh
python infer.py anchor-based --ckpt-path ../models/custom/checkpoint/custom.yml.0.pt \
  --source ../custom_data/videos/EE-bNr36nyA.mp4 --save-path ./output.mp4
```


