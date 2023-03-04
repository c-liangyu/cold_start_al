# Cold Start Problem in Vision Active Learning

![Cold Start Problem](asset/teaser.png)

Active learning promises to improve annotation efficiency by iteratively selecting the most important data to be annotated first. However, we uncover a striking contradiction to this promise: active learning fails to select data as efficiently as random selection at the first few choices. We identify this as the cold start problem in vision active learning. We seek to address the cold start problem by exploiting the three advantages of contrastive learning: (1) no annotation is required; (2) label diversity is ensured by pseudo-labels to mitigate bias; (3) typical data is determined by contrastive features to reduce outliers. 

## Paper
This repository provides the official implementation of the following paper:

<b>Making Your First Choice: To Address Cold Start Problem in Vision Active Learning</b> <br/>
[Liangyu Chen](https://c-liangyu.github.io/)<sup>1</sup>, [Yutong Bai](https://scholar.google.com/citations?user=N1-l4GsAAAAJ&hl=en)<sup>2</sup>, [Siyu Huang](https://siyuhuang.github.io/)<sup>3</sup>, [Yongyi Lu](https://scholar.google.com/citations?user=rIJ99V4AAAAJ&hl=en)<sup>2</sup>, [Bihan Wen](https://personal.ntu.edu.sg/bihan.wen/)<sup>1</sup>, [Alan L. Yuille](https://www.cs.jhu.edu/~ayuille/)<sup>2</sup>, and [Zongwei Zhou](https://www.zongweiz.com/)<sup>2</sup> <br/>
<sup>1 </sup>Nanyang Technological University,   <sup>2 </sup>Johns Hopkins University,   <sup>3 </sup>Harvard University <br/>
<i>Medical Imaging with Deep Learning (MIDL), 2023</i> <br/>
<i>NeurIPS Workshop on Human in the Loop Learning, 2022</i> <br/>
[paper](https://arxiv.org/abs/2210.02442) | [code](https://github.com/c-liangyu/CSVAL) | [poster](https://nips.cc/media/PosterPDFs/NeurIPS%202022/64383.png?t=1669951743.448019)

If you find this repo useful, please consider citing our paper:
```
@article{chen2022making,
  title={Making Your First Choice: To Address Cold Start Problem in Vision Active Learning},
  author={Chen, Liangyu and Bai, Yutong and Huang, Siyu and Lu, Yongyi and Wen, Bihan and Yuille, Alan L and Zhou, Zongwei},
  journal={arXiv preprint arXiv:2210.02442},
  year={2022}
}
```
## Installation
The selection part of code is developed on the basis of [open-mmlab/mmselfsup](https://github.com/open-mmlab/mmselfsup).
Please see [mmselfsup installation](https://mmselfsup.readthedocs.io/en/latest/install.html).

## Dataset preparation

All datasets can be auto downloaded in this repo.

MedMNIST can also be downloaded at [MedMNIST v2](https://medmnist.com/).

CIFAR-10-LT is generated in this repo with a fixed seed.

## Pretrain
Pretrain on all MedMNIST datasets
```shell
cd selection
bash tools/medmnist_pretrain.sh
```

Pretrain on CIFAR-10-LT
```shell
bash tools/cifar_pretrain.sh
```

## Select initial query
Select initial queries on all MedMNIST datasets
```shell
bash tools/medmnist_postprocess.sh
```

Select initial queries on CIFAR-10-LT
```shell
bash tools/cifar_postprocess.sh
```

## Train with selected initial query
```shell
cd training
cd medmnist_active_selection # for selecting with actively selected initial queries
# cd medmnist_random_selection # for selecting with randomly selected initial queries
# cd medmnist_uniform_active_selection # for selecting with class-balanced actively selected initial queries
# cd medmnist_uniform_random_selection # for selecting with class-balanced randomly selected initial queries
for mnist in { bloodmnist breastmnist dermamnist octmnist organamnist organcmnist organsmnist pathmnist pneumoniamnist retinamnist tissuemnist }; do bash run.sh $mnist; done
```
