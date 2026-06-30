# ai201-project3-takemeter

## Project Overview

For this project, I got information from r/hypixelskyblock, a reddit community focuses on the skyblock gamemode on the hypixel minecraft server. I split the possible posts in this community into three distinct labels.

**Labels:**
- vibes: A collection of any general community questions and people's unique experiences with the game.
    - https://www.reddit.com/r/HypixelSkyblock/comments/1uhlsyr/people_who_quit_skyblock_did_you_find_another/
    - https://www.reddit.com/r/HypixelSkyblock/comments/1uh15yr/hows_skyblock_these_days/
- opinions: People's opinions, and requests for other's opinions.
    - https://www.reddit.com/r/HypixelSkyblock/comments/1uemqhj/how_to_become_good_at_t4_emans/
    - https://www.reddit.com/r/HypixelSkyblock/comments/1uelwwk/best_early_game_crafting_flip_30mh_low_entry/
- specifics: Questions pertaining to specific game rules and mechanics.
    - https://www.reddit.com/r/HypixelSkyblock/comments/1ue87el/how_to_get_rid_of_thorns_4_on_helmet/
    - https://www.reddit.com/r/HypixelSkyblock/comments/1uibkwf/skeletons_not_counting_towards_bestiary/

Difficult to make descisions for each catagory:
- vibes: https://www.reddit.com/r/HypixelSkyblock/comments/1u9kem9/an_account_was_lost_many_tears_were_shed_and/
- opinions: https://www.reddit.com/r/HypixelSkyblock/comments/1u858tc/raffle_event_bad_timing/
- specifics: https://www.reddit.com/r/HypixelSkyblock/comments/1uhqgbd/wheat_farming_optimal_speed/

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

For my finetuning approach, I used the reccomended base model, but I did change a few parameters from the original, as the original labeling process that my data went through was even worse than the initial accuracy. The changes I made are listed below:
- 15 epochs
- 8 batching size
- 1e-5 learning rate
- 20 warmup step

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

## Fine-tuned Model Wrong analysis #1

- Failed Text: https://www.reddit.com/r/HypixelSkyblock/comments/1ubybcu/finally_realized_just_how_much_flint_i_got_from/
- True Value: vibes
- Predicted Value: specifics
- Confidence: 0.67
Explination: This error was caused due to a rhetorical question present in the post. The filter did not realize that it was rhetorical, and not intended to actually be answered. This caused the post to come off as a specific question of whether the person should do something, rather than the post's initial comical value.

## Fine-tuned Model Wrong analysis #2

- Failed Text:https://www.reddit.com/r/HypixelSkyblock/comments/1u9jag5/mushroom_farms_with_20_bps/
- True Value: specifics
- Predicted Value: opinions
- Confidence: 0.51
Explination: This question confused the system due to the fact that this was a searching question. The user was looking for something specific, hence the true label of specific. However, this question can come off as opinion, as they are asking many people for something that isn't a specific game mechanic, although having 1 correct answer, this edge case caused confusion for the system.

## Fine-tuned Model Wrong analysis #3

- Failed Text: https://www.reddit.com/r/HypixelSkyblock/comments/1uavy4t/accessories/
- True Value: specifics
- Predicted Value: opinions
- Confidence:  0.77
Explination: Honestly, I am not entirelyy sure why this example did not compute correctly. It seems pretty clearly a specifics questions to me, but my best guess as to why it was clasified as opinions is due to the user mentioning a specific example that the system was not familiar with, causing it to appear as they are asking an opinion about the topic, rather than their actual question.

## Fine-tuned Model Correct example

- Succedded text: https://www.reddit.com/r/HypixelSkyblock/comments/1u9zlvo/how_to_max_lion_pet_fast/
- True/predicted Value: opinions
- Confidence: 0.73
Explination: This makes sense to have come off as correct. This post asks a question about the "best way" to do something. While there are some ways that are definitely better than others, this question is subjective, as there are multiple different methods that could efficiently achieve the desired goal, rather than one best one.

## Reflection

