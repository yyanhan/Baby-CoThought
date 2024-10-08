# Baby-CoThought

> (This repository contains additional information for GESIS Methods Hub, [see](https://github.com/yyanhan/Baby-CoThought/blob/main/README.md#baby-cothought-for-gesis-methods-hub))


# Baby-CoThought for GESIS Methods Hub

## Description

* This project provides a method to train a language model with low training resources, where the training data is augmented by LLM. 

## Keywords

* Language model
* Low resource training
* Transformer-encoder
* Semantic similarity

## Science Usecase(s)

* when we need to calculate semantic similarity in a certain language or domain, but without a pre-trained model online, or a big training dataset, we can use this method to augment the training data. 

## Repo Structure

* `Baby-CoThought/CNLU-EG`: the code to augment training data,
* `Baby-CoThought/eval/` evaluation tools,
* `Baby-CoThought/pretrain`: the code to pretrain

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

* data in text form
* we also need an OpenAI API to augment data

## Sample Input and Output Data

* Sample Input Data: text
    ```
    Heather Wilson
        Heather Ann Wilson (born December 30, 1960) is an American politician. Wilson was the 24th United States Secretary of the Air Force from May 16, 2017 through May 31, 2019. She served as President of the South Dakota School of Mines and Technology in Rapid City,     South Dakota. She is a former Republican member of the United States House of Representatives representing from 1998 to 2009. She was the first female military veteran elected to a full term in Congress.
    After leaving Congress she was leading consulting firm Heather Wilson &amp; Company.
    On January 23, 2017, President Donald Trump announced his intentions to nominate Wilson as Secretary of the Air Force. The United States Senate confirmed her nomination on May 8, 2017.
    On March 8, 2019, Wilson said that she would resign as Secretary, on May 31, 2019, in order to become President of the University of Texas at El Paso.
    ```

* Output model: test on `https://huggingface.co/yaanhaan/Baby-CoThought`
* Sample Output: a BERT or RoBERTa language model

* Applicable DBD:
    mainly with text data, including:
  1. Historical Narratives
  2. Politicians in Wikipedia
  3. TokTrack Wikipedia
  4. Edit Histories of Wikipedia References
     
## How to Use

1. prepare your data, as long as your data is in text form. 
2. to train `RoBERTa` model, you can use
3. to augment training data with OpenAI LLM, you can use/modify [prompt](https://github.com/oooranz/Baby-CoThought/blob/main/CNLU-EG/prompts/text.py), and run this [shell code](CNLU-EG/scripts/text/cot_sampling.sh)
4. concatenate with augmented data with [code](CNLU-EG/data/text/cat_data.py) 



## Contact Details:

> Han.Yang@gesis.org


------------------


# Description of this paper

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

