# Iteration 31. Train new submission models

_25-09-2024_

## Goal

Use all the learnings from the previous iterations to train a new generation of submission models.

Do we get better scores in the leaderboard just for training for longer?

## Motivation

## Development

This is the setup that should give the best results

- Qwen2.5-0.5B-Instruct, I'm using the instruct version because of the problems with the non-instruct version
  on inference.
- Train as long as possible, do continual training (train the same model multiple times). I will first train for 40k steps, then maybe for 80k and continue with the retrainings until we don't see improvements on LB
- All datasets
- 2 tasks
- LoRA seems to generalize better, verify it on the leaderboard

## Results

[Wandb dashboard](https://wandb.ai/guillermobarbadillo/20240925_submission_models?nw=nwuserguillermobarbadillo)

## Conclusion

## Next steps

## TODO

- [ ] Using small LoRAs might open the door again to use 4 gpus for training. If training for longer is the key, this would be helpful.