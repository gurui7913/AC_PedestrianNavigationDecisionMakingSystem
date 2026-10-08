# Data availability and local source map

The repository publishes seven historical scripts, the previously public project presentation, documentation and small aggregate summaries. It does not include a complete reproducible dataset.

## Public material

| Material | Location | Scope |
|---|---|---|
| Historical scripts | `scripts/` | Original contents retained; paths reorganised |
| Original presentation | `docs/presentations/ProjectSlides_2024.pdf` | Same PDF previously published at repository root; historical claims need current caveats |
| Label-count summary | `data/summary/label_counts.csv` | Counts for three saved modelling groups; numeric direction mapping unresolved |
| Similarity summary | `data/summary/similarity_summary.json` | Descriptive statistics for one archived 13-row CSV |

The aggregate summaries cannot reproduce CLIP extraction or classifier training. Their origin is documented in [summary provenance](../data/summary/README.md).

## Material retained locally

The source folder is the existing `Term01` course archive. This source map uses its relative paths, without publishing local account names or participant identities.

| Local source | Content |
|---|---|
| `AC1_24_25_Term1_Group01_Gu_Rui/04_Source_Code/` | Submitted copies of the seven scripts; same text as the pre-reorganisation GitHub copies after newline normalisation |
| `AC1_24_25_Term1_Group01_Gu_Rui/05_Output_Appendix/lable/` | Three CSVs with 13 scene IDs and labels each |
| `AC1_24_25_Term1_Group01_Gu_Rui/05_Output_Appendix/feature/` | Three groups each of image and text feature tensors |
| `AC1_24_25_Term1_Group01_Gu_Rui/05_Output_Appendix/text/` | Original and normalised rationale files |
| `AC1_24_25_Term1_Group01_Gu_Rui/02_All_Images_and_Vector_Diagrams/` | Formal stimuli, heatmaps, processing outputs and the saved similarity CSV |
| `AC1_24_25_Term1_Group01_Gu_Rui/03_All_Videos_and_Animations/` | Session recordings and demonstrations |
| `02_DataCollection/02_Experiment/` | Task instructions, slideshow stimuli and participant-level experimental exports |
| `00_PresentationSlides/` | Presentation drafts and notes |
| `00_Feedback/` | Course feedback |
| `04_OpenSourceCodes/` | Third-party eye-tracking references; not evidence of their use as the collection system |
| `Project_Reorganisation/` | Later portfolio versions; secondary descriptions rather than raw experimental evidence |

The original local archive is preserved in place. This reorganisation creates a separate Git checkout; it does not relocate or delete original study material.

## Excluded from this update

No new participant names, face videos, audio recordings, transcripts, raw gaze exports, heatmaps, feature tensors, CV files, private interview notes or full course archive are uploaded. Raw inputs and generated model artifacts are covered by `.gitignore`; that file does not replace a review of staged files.

The existing presentation may contain third-party imagery and historical experiment examples. It was already public and remains an archival document, not a blanket release of the source data. No new consent, ethics approval or redistribution rights are asserted. Any future participant-level release requires its own consent, de-identification and source-rights review.
