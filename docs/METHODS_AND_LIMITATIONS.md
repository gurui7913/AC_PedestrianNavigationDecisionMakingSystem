# Methods, evidence and limitations

This document separates the December 2024 presentation from what the available files establish. It was added during the October 2026 repository reorganisation. It is not a report of newly trained models.

## Collection and sample accounting

The presentation describes five student participants, aged 22–23, viewing 13 formal scenes near King's Cross (8 main-road and 5 community-road scenes), with four warm-up images. The local submitted archive has five folders of 13 heatmap images.

The local modelling appendix has only three label CSVs and three groups each of image/text feature tensors, with 13 records per group. The original classifier also expects three groups. These establish 39 saved modelling records, not 65 independent training observations.

Reasons for the smaller modelling subset, the exact participant-number mapping, and the final exclusion ledger remain unresolved. The existence of a heatmap file is not evidence that the underlying trial met a predefined quality criterion.

Saved label counts are:

| Label value | Group 1 | Group 2 | Group 3 | Total |
|---|---:|---:|---:|---:|
| 0 | 2 | 6 | 3 | 11 |
| 1 | 9 | 5 | 9 | 23 |
| 2 | 2 | 2 | 1 | 5 |
| Total | 13 | 13 | 13 | 39 |

The study instructions mention straight/left/right responses, but the numeric encoding dictionary is not verified. Do not attach direction names to these numeric counts without recovering that mapping.

With default three-class balancing, SMOTE would increase these counts to 23 per class (69 total), including 30 synthetic vectors. This is arithmetic implied by the saved labels and settings, not a reproduced training run. Synthetic vectors are not additional participants or observed decisions.

## Measurement and task design

- The study used Gaze Recorder. Reference eye-tracker repositories and proposed custom OpenCV work do not establish that a custom tracking system was used for collection.
- The presentation shows calibration options with 3/5/9/16 targets. Per-session settings and quantitative validation errors have not been recovered, so no fixed calibration count, sampling rate or angular accuracy is asserted.
- The experiment precaution document requests 15-second slide intervals. The three saved formal PPTX decks contain 13 slides with 10-second automatic-transition settings. Actual execution timing still requires recording review.
- Instructions asked participants to avoid prolonged reading of street names on the road. This task constraint matters when interpreting responses to signage.
- An explicit randomisation/counterbalancing record and a complete raw-coordinate-to-fixation-chart calculation chain have not been established.
- Static scene choices cannot directly establish real-world routes, navigation success, cognitive decline or causal effects of an environmental feature.

## Implementation checks

### Feature construction

The visual script encodes the original image and focus/heatmap image separately with pretrained CLIP ViT-B/32, then combines their vectors. The text script independently encodes each line of description. Representative saved tensors are 1×512, implying a 1024-dimensional concatenated classifier input.

The HSV contour script and image-difference script are inspection utilities. They do not establish semantic attention categories, validated fixation events or a learned heatmap predictor. The image-combination weight is selected by whether a filename contains `red`, not by a recovered gaze-weighting model.

### Feature–label alignment

The training script reads image features, text features and labels independently and concatenates them by position. It does not join by participant and scene ID. The current local file enumeration differs from the saved CSV order; the historical execution order is unknown.

Sorting feature filenames alone is not a correction. A new analysis needs a checked manifest linking participant, scene, text line, feature filename and label, with uniqueness and missing-pair checks.

### Evaluation

The script resamples the entire dataset before cross-validation and before the held-out split. [imbalanced-learn documents this as data leakage](https://imbalanced-learn.org/dev/common_pitfalls.html). Neither evaluation output is made independent by calling one of them a test-set score. The magnitude of any score inflation has not been measured here.

Repeated records from the same participant and repeated views of the same scene create dependencies. New-participant and new-scene performance are different questions and require separate grouped evaluations. See [scikit-learn's grouped cross-validation guidance](https://scikit-learn.org/stable/modules/cross_validation.html).

Descriptions are collected with decisions and include direction information, even in some normalised text. They may be legitimate inputs to a clearly defined retrospective response-classification task; they do not establish prediction before a participant makes a choice. The provenance of every saved text tensor also needs confirming.

## What can be reported

- An exploratory study connecting static scenes, gaze heatmaps and spoken wayfinding rationales.
- The saved modelling subset and its numeric label counts.
- The descriptive mean/range of the specific 13-row saved similarity file, with its limited provenance.
- The actual feature-processing and classifier steps implemented in the archived scripts.

The original presentation's approximate 80% accuracy and 50% baseline are retained only as historical claims. Exact run logs, splits, predictions and comparator definitions are insufficient to substantiate a validated performance comparison. Earlier README descriptions of 86.96% CV accuracy, exact calibration, saved model artifacts, unsupported CLI commands and an implemented ViT decoder are not substantiated by the archived scripts and are removed from the current documentation.

Positive cosine similarity is not a statistical test of gaze–reasoning agreement. No matched-pair versus shuffled-pair comparison, task-specific calibration or independently verified behavioural association is established by the available similarity CSV alone. No validated cue hierarchy or significance test is claimed.

## Proposed reanalysis, not completed work

1. Recover the participant–scene manifest, numeric label dictionary, text provenance and exclusions.
2. Define the task and prediction time point, including whether verbal rationales are available at inference.
3. Align inputs by explicit IDs. Check complete one-to-one pairing and fit all learned transformations on training data only.
4. Evaluate unseen participants and unseen scenes separately; keep original observations in test folds.
5. Compare a training-defined majority-class baseline, image-only, text-only and combined-feature models on the same splits. Prefer simple alternatives before assuming SMOTE helps this very small dataset.
6. Report class counts, per-class metrics, confusion matrices, per-group results and uncertainty. Recovering only three modelling participants will still limit inference.
7. Label any new results with their actual analysis date. Do not attribute a 2026 correction to the original 2024 study.
