# Baby-CoThought

> (This repository with additional information for GESIS Methods Hub)

[![Model](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Model-blue)](https://huggingface.co/yaanhaan/Baby-CoThought)
[![Model](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Data-green)](https://huggingface.co/datasets/yaanhaan/Baby-CoThought-Data)
[![arXiv](https://img.shields.io/badge/arXiv-2305.12182-b31b1b.svg)](https://arxiv.org/abs/2308.01684)

This repository contains the code for the paper: 

>[Baby's CoThought: Leveraging Large Language Models for Enhanced Reasoning in Compact Models](https://aclanthology.org/2023.conll-babylm.13/). 

In this work, we apply our "CoThought" pipeline to pretrain a Baby Language Model (BabyLM) with human-like smaller corpus data.

The pretraining data is provided by [Warstadt et al. (2023)](https://arxiv.org/abs/2301.11796) in the framework of the [BabyLM Challenge](https://babylm.github.io/), which has the goal of sample-efficient pretraining on a developmentally plausible corpus at a small human-like data scale.

![](./figures/baby-cothought.png)

## Contents

- `CNLU-EG`: Contains the code for the Creative NLU-Example Generation (CNLU-EG).
- `pretrain`: Contains the code and instructions for pretraining RoBERTa model.
- `eval`: Contains the code for a shared evaluation pipeline from [Warstadt et al. (2023)](https://arxiv.org/abs/2301.11796).

## Creative NLU-Example Generation
1. Download [babylm_data](https://github.com/babylm/babylm.github.io/raw/main/babylm_data.zip), run `./CNLU-EG/data/text/cat_data.py` to merge them.
    ```bash
    cd ./babylm_data/babylm_100M
    cat aochildes.train bnc_spoken.train cbt.train cbt.train children_stories.train open_subtitles.train qed.train switchboard.train > merged_data.txt
    python cat_data.py merged_data.txt text.txt
    ```
   Then we can get the raw data for the next step.
2. Use LLMs to generate the new dataset consisting of NLU-Examples.
    ```bash
    cd ./CNLU-EG/scripts/text
    bash cot_sampling.sh
    ```
   
## Pre-Train the BabyLM
- Pre-train the BabyLM with our generated dataset. 
- The generated dataset can be downloaded from [here](https://huggingface.co/datasets/yaanhaan/Baby-CoThought-Data).
   ```shell
   cd ./pretrain
   python RoBERTa.py RoBERTa_config.json
   ```

## Evaluation
- Evaluate the trained BabyLM on a shared pipeline, hosted at [this GitHub link](https://github.com/babylm/evaluation-pipeline ).
- The public validation data utilized is a blend of BLiMP and (Super)GLUE tasks. Additional tasks will be held out for the final evaluation of submitted models.


## Citation

If you found the resources in this repository useful, please cite:

```
@inproceedings{zhang-etal-2023-babys,
    title = "Baby{'}s {C}o{T}hought: Leveraging Large Language Models for Enhanced Reasoning in Compact Models",
    author = {Zhang, Zheyu  and
              Yang, Han  and
              Ma, Bolei  and
              R{\"u}gamer, David  and
              Nie, Ercong},
    editor = "Warstadt, Alex  and
              Mueller, Aaron  and
              Choshen, Leshem  and
              Wilcox, Ethan  and
              Zhuang, Chengxu  and
              Ciro, Juan  and
              Mosquera, Rafael  and
              Paranjabe, Bhargavi  and
              Williams, Adina  and
              Linzen, Tal  and
              Cotterell, Ryan",
    booktitle = "Proceedings of the BabyLM Challenge at the 27th Conference on Computational Natural Language Learning",
    month = dec,
    year = "2023",
    address = "Singapore",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.conll-babylm.13",
    pages = "130--142",
}
```

# Baby-CoThought for GESIS Methods Hub

## Description

* Provide a brief and clear description of the method, its purpose, and what it aims to achieve. Add a link to a related paper from social science domain and show how your method can be applied to solve that research question. For example, 4TCT is a specialized tool designed for the efficient collection of textual data from the 4chan platform. It automates the process of gathering posts from various boards, aiming to facilitate research and analysis in social science and computational linguistics. This tool is particularly useful for analyzing online discourse, community dynamics, and trends within the 4chan ecosystem. It can support studies on topics like meme culture, information dissemination, and the impact of anonymous social media on public opinion.

## Keywords

* Language model
* Low resource training
* Transformer-encoder
* Semantic similarity

## Science Usecase(s)

* Include usecases from social sciences that would make this method applicable in a certain scenario. The use cases or research questions mentioned should arise from the latest social science literature cited in the description. For example, How to collect 4chan data from on political discourse from dates ..

## Repo Structure

* Explain the overall structure of the method, including directories, key files, and their functions. For example, The tool's architecture includes a src/ directory for core scripts, with requester.py handling data collection, board.py managing board-specific requests, and utils.py for auxiliary functions. Data is stored in a data/ directory created upon initiation, and documentation is available in docs/.

## Environment Setup

* Python 3.8
* install the following packages:  
    ```
    torch
    tokenizers
    transformers
    openai
    ```
## Input Data
1. data in text form

## Sample Input and Output Data

   
## How to Use

1. prepare your data, as long as your data is in text form. 
2. 

## Contact Details:

> Han.Yang@gesis.org

