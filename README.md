# Baby-CoThought

This repository contains the code for the paper: 

["Baby's CoThought: Leveraging Large Language Models for Enhanced Reasoning in Compact Models"](https://arxiv.org/pdf/2308.01684v1.pdf). 

In this work, we apply our "CoThought" pipeline to pretrain a Baby Language Model (BabyLM) with human-like smaller corpus data.

The pretraining data is provided by [Warstadt et al. (2023)](https://arxiv.org/abs/2301.11796) in the framework of the [BabyLM Challenge](https://babylm.github.io/), which has the goal of sample-efficient pretraining on a developmentally plausible corpus at a small human-like data scale.

The restructured data for BabyLM pretraining is available [here](https://huggingface.co/datasets/yaanhaan/Baby-CoThought-Data).

Our BabyLM is available [here](https://huggingface.co/yaanhaan/Baby-CoThought).

![](./figures/baby-cothought.png)

## Contents

- `CNLU-EG`: Contains the code for the Creative NLU-Example Generation (CNLU-EG).
- `pretrain`: Contains the code and instructions for pretraining RoBERTa model.

## Citation

If you found the resources in this repository useful, please cite:

```
@misc{zhang2023babys,
      title={Baby's CoThought: Leveraging Large Language Models for Enhanced Reasoning in Compact Models}, 
      author={Zheyu Zhang and Han Yang and Bolei Ma and David Rügamer and Ercong Nie},
      year={2023},
      eprint={2308.01684},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```
