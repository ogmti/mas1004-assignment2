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
- what tells the cities apart: 각 나라는 도시 사진 속 간판 언어의 차이에 따라 쉽게 구분할 수 있지만 간판이 없는 사진도 있기 때문에 글자 외의 요인에 의한 구분이 필요하다. 같은 나라 안의 도시는 기준을 찾기 어려웠으며 도시의 거리와 직접적으로 연관되지 않은 박물관 유물이나 자동차 실내 사진 등이 있었다. 단, 부산의 경우 바다가 자주 나오는 등의 경향을 통해 기준을 잡을 수 있었다.

## 2026-11-10 baseline (Track A), not finished
- `official.py --tag baseline` on mps stopped with "RuntimeError: view size is not compatible with input tensor's size and stride" (`results/logs/baseline_seed0_mps_failed.log`)
- the same run on cpu started and did not finish; no row in `experiments.csv` (`results/logs/baseline_seed0.log`)

## 2026-11-10 starter recipe release (Track A)
- `official.py --quick --device cpu` passed (validation 0.241 on 200 photos; on mps the same error as above)
- released `track-a-1` "starter recipe" (`track_a/recipe.py` unchanged, no `selection.csv`)
- why: 레시피를 바꾸기 전에 아무 변화 없는 결과를 기준으로 삼고 릴리스가 리더보드에 올라가는지 확인하기 위해 기본 레시피를 먼저 냈다. Colab GPU를 받지 못해 학습 없이 빠른 점검만 하고 릴리스했다.

## 2026-11-10 starter_b (Track B)
- changed: `src/train_b.py` as given (resnet18, 224 px, 4 epochs, starter training photos, IMAGENET1K_V1), `--tag starter_b --submit`, on mps, 1144 s of training
- why: Track B의 경우 시간 부족으로 인해서 train_b.py를 그대로 학습해야만 했다.
- validation: 0.4926 (seoul 0.5363, busan 0.3755, tokyo 0.6284, osaka 0.3745, taipei 0.5484); no Track B run before
- `check_submission.py`: format and limits: OK, 11.17 million parameters, 1.81 billion multiply-adds, score 0.493 on 12077 photos
- released `track-b-1` "starter model"
- what it means: 오사카 사진이 눈에 띈다. 이로부터 같은 나라 안의 도시는 기준을 찾기 어렵다는 기준을 도출해낼 수 있다고 생각했지만 도쿄 사진을 오사카로 착각한 것은 적었고, 마찬가지로 서울과 부산의 경우도 이와 비슷했다.

## 2026-11-10 baseline (Track A)
- changed: starter recipe as given, all training photos, seeds 0 and 1, on Colab (cuda)
- why: 우연함만으로 점수가 얼마나 움직이는지를 관찰하려고 했다.
- validation: seed 0 0.4919 (seoul 0.5737, busan 0.3806, tokyo 0.6174, osaka 0.3398, taipei 0.5479); seed 1 0.4909 (seoul 0.5630, busan 0.3986, tokyo 0.6138, osaka 0.3689, taipei 0.5105); no full Track A run before
- `curate.py mistakes` on baseline seed 0 (`results/curate/mistakes_baseline_seed0_*`): wrong on seoul 1038 of 2435, busan 859 of 1390, tokyo 1485 of 3881, osaka 1404 of 2128, taipei 1013 of 2243
- two things the mistakes have in common: 차량이 등장하는 이미지이거나 사람들이 여럿 나오는 이미지가 많다.
- what it means: 같은 나라 안의 도시는 기준을 찾기 어렵다.

## Not done (time ran out)
- PLAN Step 5: a Track A release by the mid-point check (30 October); the first release is from 10 November
- PLAN Step 6: Track A changes, one at a time
- PLAN Step 7: dropping photos by my own rule
- PLAN Step 9: Track B changes after the first model

## Next
시간이 더 주어지면 왜 틀리는지 보고, 하나를 바꾸고, 점수가 올랐는지 재는 과정을 거치고 싶다.
