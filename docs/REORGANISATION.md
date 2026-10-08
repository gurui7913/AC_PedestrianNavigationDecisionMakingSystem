# Repository reorganisation — 2026-10-08

## Scope

This is a maintenance and documentation update to the 2024 course project. It introduces no new trained model, no corrected accuracy score and no claim that the original evaluation issues are fixed.

The README is rewritten to match the available code and local archive. Nonexistent CLI interfaces and output artifacts, unsupported class counts, calibration details and model-performance claims are removed. The original PDF is retained with explicit historical context. Prior README versions remain available in Git history.

## File mapping

| Before | After |
|---|---|
| `Image and Heatmap Analysis/highlight_visual_differences.py` | `scripts/01_heatmap_processing/highlight_visual_differences.py` |
| `feture_extraction/extract_visual_attention.py` | `scripts/01_heatmap_processing/extract_visual_attention.py` |
| `Image and Heatmap Analysis/image_text_feature_analysis.py` | `scripts/02_feature_extraction/image_text_feature_analysis.py` |
| `feture_extraction/text_feature_extraction.py` | `scripts/02_feature_extraction/text_feature_extraction.py` |
| `Similarity Analysis/feature_similarity_analysis.py` | `scripts/03_similarity_analysis/feature_similarity_analysis.py` |
| `Model Training/train_path_choice_model_en.py` | `scripts/04_model_training/train_path_choice_model_en.py` |
| `Visualization/visualize_similarity.py` | `scripts/05_visualization/visualize_similarity.py` |
| `ProjectSlides.pdf` | `docs/presentations/ProjectSlides_2024.pdf` |

The scripts and PDF have unchanged contents relative to their pre-reorganisation Git blobs. New explanatory material is outside these archived files.

## Validation scope

The update checks source preservation, Python syntax without executing module-level code, repository-local documentation links, staged file content, aggregate arithmetic against local source CSVs, and excluded private-artifact patterns. It does not install the ML dependency stack, download CLIP weights, run model inference, train a classifier or verify every session recording.

The new dependency list records imports used by the archived scripts. It is not a tested or historical version lockfile. The code-reading guide states the path placeholders and unresolved stage handoffs explicitly.
