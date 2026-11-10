# Log

One entry for each recipe, selection or Track B model you train, newest at
the bottom. The numbers come from `experiments.csv`. "Why" and "what it means"
are in your own words: your agent asks you for them and does not make them up.
End the log with your plan for what to try next.

<!-- The form of an entry:

## <date> <tag> (Track A or B)
- changed: what is different from the run before
- why: your reason
- validation: 0.000 (before: 0.000)
- what it means: what you think the result says
-->

## 2026-11-05 setup check (Track A, --quick)
- changed: starter recipe as given, `official.py --quick` (20 steps, cpu)
- validation: 0.241 (200 validation photos, not an official run)

## 2026-11-09 looking at photos
- `curate.py look` sheets made for all five cities (`results/curate/look_*`)
- what tells the cities apart:

## 2026-11-10 baseline (Track A), not finished
- `official.py --tag baseline` on mps stopped with "RuntimeError: view size is not compatible with input tensor's size and stride" (`results/logs/baseline_seed0_mps_failed.log`)
- the same run on cpu started and did not finish; no row in `experiments.csv` (`results/logs/baseline_seed0.log`)

## 2026-11-10 starter recipe release (Track A)
- `official.py --quick --device cpu` passed (validation 0.241 on 200 photos; on mps the same error as above)
- released `track-a-1` "starter recipe" (`track_a/recipe.py` unchanged, no `selection.csv`)
- why:
- what it means:

## 2026-11-10 starter_b (Track B)
- changed: `src/train_b.py` as given (resnet18, 224 px, 4 epochs, starter training photos, IMAGENET1K_V1), `--tag starter_b --submit`, on mps, 1144 s of training
- why:
- validation: 0.4926 (seoul 0.5363, busan 0.3755, tokyo 0.6284, osaka 0.3745, taipei 0.5484); no Track B run before
- `check_submission.py`: format and limits: OK, 11.17 million parameters, 1.81 billion multiply-adds, score 0.493 on 12077 photos
- released `track-b-1` "starter model"
- what it means:

## Not done (time ran out, and no Colab GPU could be allocated)
- PLAN Step 2: baseline with seeds 0 and 1 (no full Track A run finished)
- PLAN Step 3: mistakes of the baseline
- PLAN Step 5: a Track A release by the mid-point check (30 October); the first release is from 10 November
- PLAN Step 6: Track A changes, one at a time
- PLAN Step 7: dropping photos by my own rule
- PLAN Step 9: Track B changes after the first model

## Next
