# :taco: TACO -- Twitter Arguments from COnversations

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.8030026.svg)](https://doi.org/10.5281/zenodo.8030026)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com)

[![Share to Community](https://huggingface.co/datasets/huggingface/badges/raw/main/powered-by-huggingface-dark.svg)](https://huggingface.co/TomatenMarc/TACO)

This repository contains the annotation framework, dataset and code used for the resource paper *"TACO -- Twitter Arguments from COnversations"*.
To use the baseline model, please visit [Hugging Face](https://huggingface.co/TomatenMarc/TACO).

**Table of Contents:**

- [Repository Layout](#repository-layout)
- [Findings](#findings)
- [Example](#example-conversation)
- [Licensing](#licensing)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

## Repository Layout

1. [data](./data)
    1. [README.md](./data/README.md): A data-specific README for TACO and its annotation process.
    2. [annotation_framework.pdf](./data/annotation_framework.pdf): The annotation framework for TACO.
    3. [conversations.csv](./data/conversations.csv): Having stored the structure of all collected conversations.
    4. [majority_votes.csv](./data/majority_votes.csv): All the majority votes, which serve as the labeled ground truth.
    5. [worker_decisions.csv](./data/worker_decisions.csv): All individual expert decisions.
2. [notebooks](./notebooks)
    1. [dataset_statistics.ipynb](./notebooks/dataset_statistics.ipynb): For comparing the dataset statistics.
    2. [classifier_cv.ipynb](./notebooks/classifier_cv.ipynb): For training and evaluating the baseline model.
3. [outputs](./outputs)
    1. [bertweet_cv_predictions.csv](./outputs/bertweet_cv_predictions.csv): The ground truth and cross-validation results of the baseline model.

## Findings

### Sample Distribution

                     sample       total            query-time        key-date
    Abortion         486 (26.8%)   29,939  (5.0%)  2021/08/15-10/16  S.B.8 took effet on 2021/09/01.
    Brexit           535 (29.5%)  427,260 (70.9%)  2020/01/01-03/01  Brexit took effect on 2020/02/01.
    GoT              192 (10.6%)   61,705 (10.2%)  2019/04/01-05/01  GOT S8 premiered (HBO-US) on 2019/04/19.
    LOTRROP          209 (11.5%)   14,014  (2.3%)  2022/02/01-03/01  LOTRROP teaser trailer was released on 2022/02/14.
    SquidGame        226 (12.5%)   51,215  (8.5%)  2021/09/10-10/10  Squid Game was released (Netflix wordlwide) on 2021/09/17. 
    TwitterTakeover  166  (9.1%)   18,531  (3.1%)  2022/04/01-05/01  Elon Musk offers $43 billion to purchase Twitter on 2020/04/14.

### Dataset Distribution

      Argument                    No-Argument
      865 (49.88%)                869 (50.12%)
      
      Reason       Statement      Notification  None
      581 (33.50%) 284 (16.38%)   500 (28.84%)  369 (21.28%)

### Conversational Reply Patterns

                  Reason  Statement   Notification    None
          Reason    0.51       0.12           0.31    0.06
       Statement    0.38       0.21           0.33    0.08
    Notification    0.26       0.08           0.57    0.09
            None    0.26       0.08           0.44    0.22

### Performance Multi-Class Classification Task (BERTweet)

                    precision    recall  f1-score   support
            Reason     0.7369    0.7522    0.7445       581
         Statement     0.5437    0.5915    0.5666       284
      Notification     0.7902    0.7760    0.7830       500
              None     0.8387    0.7751    0.8056       369

          accuracy                         0.7376      1734
         macro avg     0.7274    0.7237    0.7249      1734
      weighted avg     0.7423    0.7376    0.7395      1734

### Performance Binary Classification Task (BERTweet)

                   precision    recall  f1-score   support
      No-Argument     0.8666    0.8297    0.8477       869
         Argument     0.8359    0.8717    0.8534       865

         accuracy                         0.8506      1734
        macro avg     0.8513    0.8507    0.8506      1734
     weighted avg     0.8513    0.8506    0.8506      1734

### Textual Features

                       Reason Statement Notification      None
      Average Length      213       122          156        63
                URLs    34.6%      8.1%        71.6%      7.6%
       external URLs    41.8%     17.4%        49.7%     17.9%
              Emojis    11.9%     14.1%        16.0%     35.8%
            Hashtags    45.8%     38.7%        60.0%     12.2%
               Users    65.9%     68.0%        56.4%     91.3%
    Discourse Marker    32.9%     19.0%        11.4%      8.7%

### Error Analysis

                  Reason  Statement   Notification   None
          Reason     437         76             66      2
       Statement      73        168             13     30
    Notification      63         26            388     23
            None      20         39             24    286

## Example Conversation

<div align="center">
  <img src="https://github.com/TomatenMarc/public-images/raw/main/taco_conversation.svg" alt="Component Space" width="100%">
</div>

## Licensing

<p>
  <a property="dct:title" rel="cc:attributionURL" href="https://github.com/TomatenMarc/TACO">TACO -- Twitter Arguments from Conversations</a> by 
  <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="mailto:marc.feger@uni-duesseldorf.de">Marc Feger</a> is licensed under 
  <a href="http://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0</a>
  <div style="display:block;">
    <img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1">
    <img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1">
    <img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1">
    <img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1">
  </div>
</p>

## Contact

Please contact [marc.feger@uni-duesseldorf.de](mailto:marc.feger@uni-duesseldorf.de) or [stefan.dietze@gesis.org](mailto:stefan.dietze@gesis.org).

## Acknowledgements

We thank Aylin Martin, Tillmann Junk, Andreas Burbach, Talha Caliskan, and Aaron Schneider for their contributions to the
annotation process in this paper.
