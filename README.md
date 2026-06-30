# ai201-project3-takemeter

## Project Overview

For this project, I got information from r/hypixelskyblock, a reddit community focuses on the skyblock gamemode on the hypixel minecraft server. I split the possible posts in this community into three distinct labels.

**Labels:**
- vibes: A collection of any general community questions and people's unique experiences with the game.
- opinions: People's opinions, and requests for other's opinions.
- specifics: Questions pertaining to specific game rules and mechanics.

## Evaluation Report

Baseline Model overall accuracy: 0.767
|         |precision |reacall |f1-score |support |
|---------|----------|-------|---------|--------|
| vibes| 0.75| 1.00| 0.86| 6|
| opinions| 1.00| 0.46| 0.63| 13|
| specifics| 0.69| 1.00| 0.81| 11|
| accuracy| | | 0.77| 30|
| macro avg| 0.81| 0.82| 0.77| 30|
| weighted avg| 0.84| 0.77| 0.74| 30|


Fine tuned Model overall accuracy: 0.33
|         |precision |reacall |f1-score |support |
|---------|----------|-------|---------|--------|
| vibes| 1.00| 0.17| 0.29| 6|
| opinions| 0.42| 0.62| 0.50| 13|
| specifics| 0.10| 0.09| 0.10| 11|
| accuracy| | | 0.33| 30|
| macro avg| 0.51| 0.29| 0.29| 30|
| weighted avg| 0.42| 0.33| 0.31| 30|

Fine tuned model confusion matrix:
|vibes(True)|1|1|4|
|--------------------|:--------------------:|:--------------------:|:--------------------:|
|opinions(True)|0|8|5|
|specifics(True)|0|10|1|
||vibes(Predicted)|opinions(predicted)|specifics(predicted)|