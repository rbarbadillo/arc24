# Iteration 47. Select instead of verify

_29-10-2024_

## Goal

Can I improve prediction selection if instead of verifying the correctness I select between pairs of predictions?

## Motivation

We have seen that verifying the predictions has predictive power and is a method that can improve
over voting in some situations. But it is not improving the leaderboard score.

Maybe the problem is that if many predictions are considered correct by the model, there is no
way to separate them just by verifying. However if we compare those predictions directly and ask
the model to select the best one, in that case it is possible that we could discriminate the predictions.

## Development

### Create select predictions script

```
export checkpoint_folder=/mnt/hdd0/Kaggle/arc24/models/20241026_improve_verifiers/01_verify-and-select_lora032-Qwen2-0.5B-Instruct_lr5e-5_bs32_16000steps_2gpus_8192msl/checkpoint-16000
python easy_select_and_evaluation.py "${checkpoint_folder}" \
--dataset-path /mnt/hdd0/Kaggle/arc24/data/new_partitions/arc-agi_all_challenges.json \
--predictions-path  /mnt/hdd0/Kaggle/arc24/debug/01_full-fine-tuning-Qwen2-0.5B-Instruct_lr5e-5_8e4steps_2gpus_8192msl_checkpoint-80000_inference_evaluation_x032_just_correct_tasks.json \
--verifications-per-prediction 4
```

## Results

### Analyze submission

On this [notebook](https://www.kaggle.com/code/ironbar/test-2020-solution-script?scriptVersionId=192932864) the 2020 solution
is used with just 1 attempt (the 2 attempt is empty) and scores 24. With [2 attempts](https://www.kaggle.com/code/ironbar/test-2020-solution-script?scriptVersionId=192884747)
it scores 26.

### Analyze verifications

I have studied the failed verifications and found that 36% of them fail with ties. If I can use
the select mode instead to fix that I might have a better prediction selection mode.

## Conclusion

## Next steps

- If I define some correctness metric over the predictions, that could open the door to a much more
  training dataset that won't be using the correct prediction over an over. It is unclear if this
  would work better.
- Test time fine-tuning could be use to train a verifier, if wrong predictions are created for the
  the test data.

## TODO

- [x] I need more information to understand the failures of verifying. I need to save the results of the verifications for
  deeper analysis.
- [ ] Create a first script to do prediction selection with comparisons. First do an all vs all comparison.
- [ ] Update the script to be more efficient and do more selective comparisons, using maybe trueskill.