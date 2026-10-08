# Presentation images used in the README

These images are direct full-page renders of the [previously public December 2024 presentation](../presentations/ProjectSlides_2024.pdf). They preserve the original layout, embedded captions and any credits visible on each selected page. No new private experiment files were used.

| Image | Source page | Use |
|---|---:|---|
| `01_project_cover.jpg` | 1 | Project title, team and course context |
| `02_study_site.jpg` | 12 | King's Cross study setting |
| `03_street_view_stimuli.jpg` | 13 | Warm-up and formal street-view stimuli |
| `04_gaze_and_rationales.jpg` | 16 | Gaze heatmap examples alongside reported choices |
| `05_heatmap_processing.jpg` | 23 | Historical image-processing illustration, in an expandable section |

Exports: Poppler `pdftoppm`, JPEG quality 90, maximum dimension 1600 pixels, original page aspect ratio, no cropping or content changes. The five images total approximately 1.3 MB. Exact source and image hashes are recorded in [manifest.json](manifest.json).

For example, render page 12 from the repository root:

```bash
pdftoppm -f 12 -l 12 -scale-to 1600 -jpeg -jpegopt quality=90 -singlefile docs/presentations/ProjectSlides_2024.pdf docs/images/02_study_site
```

The README supplies current context beneath each image. These archival examples do not validate model performance, causal cue effects, fixation-duration measurements or a heatmap-generating model. Pages claiming classification accuracy or heatmap prediction are not used in the gallery.

The original deck includes third-party street imagery and other credited material. Exporting its pages does not create new redistribution rights or change existing attribution. Consult the source presentation and [data availability](../DATA_AVAILABILITY.md).
