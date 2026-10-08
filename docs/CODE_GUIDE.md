# Code guide

The seven scripts are the archived team implementation. The October 2026 change reorganises their paths and documentation; it does not fix their algorithms or reproduce their results. Script contents are unchanged from the repository before reorganisation.

All scripts execute at module level. Reading them does not require installing ML dependencies, but importing them can trigger file operations, model downloads or training. They are not a Python library or a command-line application.

## Recommended reading order

### 1. Heatmap inspection

[`highlight_visual_differences.py`](../scripts/01_heatmap_processing/highlight_visual_differences.py)

- Configure `original_image_path`, `heatmap_image_path`, `output_path`.
- Matches image names, centre-crops the heatmap to at most 800×450, resizes it to the original image, computes absolute image differences, thresholds at 50 and creates a colour overlay.
- Writes `highlighted_<image filename>` images.
- This is image processing, not gaze-coordinate calibration. Cropping, resizing, compression and background differences can affect the result; inspect spatial registration before interpreting hotspots.

[`extract_visual_attention.py`](../scripts/01_heatmap_processing/extract_visual_attention.py)

- Configure `heatmap_image_path`, `output_path`.
- Uses HSV ranges to detect red and green regions, applies morphology to the green mask, and draws contours.
- Writes `highlighted_<image filename>` images.
- Does not identify semantic categories such as buildings or trees, calculate fixation durations, or apply a learned attention model. Scene colours can be confused with heatmap colours.

### 2. Visual feature extraction

[`image_text_feature_analysis.py`](../scripts/02_feature_extraction/image_text_feature_analysis.py)

Despite its name and inherited header description, this file extracts **image** features, not text features.

- Configure `original_image_path`, `focus_area_path`, `output_feature_path`.
- Loads pretrained CLIP ViT-B/32 and preprocesses the original image and corresponding focus/heatmap image separately.
- Uses `encode_image` under `torch.no_grad()`; there is no CLIP training loop.
- Calculates `(original_features + weight * focus_features) / 2`.
- `weight` is 1.5 if the base filename contains `red`, otherwise 1.0. This is a filename-dependent heuristic, not pixel-wise attention weighting.
- Writes `<image stem>_features.pt`; representative local files contain a 1×512 float tensor.
- The script does not explicitly L2-normalise vectors before saving. Check inputs and preprocessing rather than assuming HSV output is a special CLIP channel.

### 3. Text feature extraction

[`text_feature_extraction.py`](../scripts/02_feature_extraction/text_feature_extraction.py)

- Configure `descriptions_path`, `output_path`.
- Reads each `.txt` file line by line, tokenises each stripped line and calls CLIP `encode_text` without fine-tuning.
- Writes `<description filename>_desc_<zero-based line index>_features.pt`.
- Text normalisation is not performed by this script beyond stripping whitespace. Original and separately normalised text files existed in the local archive; which version produced every saved tensor is not fully established.
- Blank lines are not skipped. Input line count and line-to-scene mapping need checking.

**Handoff gap:** saved local text tensors were renamed to `imageN_features.pt`, but this renaming/mapping is not implemented here. Similarity analysis expects matching image IDs. Create an explicit mapping before attempting to connect stages; never rely on renaming by guesswork.

### 4. Image–text similarity

[`feature_similarity_analysis.py`](../scripts/03_similarity_analysis/feature_similarity_analysis.py)

- Configure `image_features_path`, `text_features_path`, `output_csv_path`.
- Selects `_features.pt` files, sorts filenames lexicographically, pairs them using `zip`, and checks the portion before the first underscore.
- Loads tensors and computes cosine similarity using scikit-learn.
- Writes CSV columns `image_file`, `text_file`, `similarity`.
- `zip` truncates unequal lists; the filename check is not a participant–scene join. Same names also do not prove that a renamed text tensor corresponds to the correct explanation.
- Cosine similarity describes feature-space proximity, not statistical significance or choice-prediction accuracy.

### 5. Route-choice classification

[`train_path_choice_model_en.py`](../scripts/04_model_training/train_path_choice_model_en.py)

- Configure all three entries in each of `visual_features_folders`, `text_features_folders`, and `labels_files`.
- These entries are literal placeholder strings, not calls to `input()`; there are no CLI flags.
- Concatenates visual tensors into rows, text tensors into rows, and joins the two matrices by column position. Representative inputs imply 39×1024 features before oversampling.
- Reads each label CSV's `label` column without using `image_id` to align it to feature rows.
- Runs `SMOTE(random_state=42, k_neighbors=4)` on the complete matrix.
- Defines `RandomForestClassifier(n_estimators=200, max_depth=10, random_state=42)`.
- Calls 3-fold `cross_val_score`, then an 80/20 `train_test_split` of the already resampled matrix, fits the model and prints accuracy/confusion matrix.
- Does **not** save a trained model, prediction table or classification-report file.

Do not use this unchanged script to support a new performance claim: ID alignment, train-only resampling and grouped evaluation require correction. With only five original records in one class, training-fold SMOTE with `k_neighbors=4` may also be infeasible; it must not be copied into every fold blindly.

### 6. Similarity plot

[`visualize_similarity.py`](../scripts/05_visualization/visualize_similarity.py)

- Configure `similarity_file_path`, `output_chart_path`.
- Reads the similarity CSV, plots a bar for each row, saves the plot and calls `plt.show()`.
- Does not generate road-type breakdowns or classification performance charts.

## Explaining the model accurately

1. Pretrained CLIP provides visual and language representations.
2. Scene and heatmap image vectors are averaged; the text vector is concatenated for classification.
3. Random Forest is the supervised classifier; CLIP is not fine-tuned.
4. The original target contains three numeric label values; their exact direction dictionary must be confirmed.
5. Verbal rationales come with the choices, so the setup does not establish prospective prediction from scenes alone.
6. The scripts do not implement a heatmap-generating ViT decoder or text generation.

See [methods and limitations](METHODS_AND_LIMITATIONS.md) before discussing historical accuracy.
