# EDA: PAD-UFES-20

Exploratory data analysis for the ADLM project
[adlm-multimodal-uncertainty](https://github.com/ADLM-Multimodal-Uncertainty/adlm-multimodal-uncertainty):
does clinical metadata reduce the epistemic uncertainty of a skin-lesion image classifier?

Notebooks are fine here, because this repo is for exploring. Anything reusable (splits, metadata
encoding) moves to the main repo; preprocessing and training never run from notebooks.

## Layout

```
data/        local copy of the dataset, not committed
notebooks/   exploration notebooks (clear outputs before committing large ones)
figures/     figures for slides and report
tables/      CSV tables behind the figures
docs/
  eda_plan.md             what we analyse and the findings so far
  first_pass_summary.md   tables from the first pass over metadata.csv
```

## Key findings so far (metadata only)

- 2298 images, 1373 patients; `lesion_id` is only unique within a patient, so splits are grouped by patient.
- Classes: BCC 845, ACK 730, NEV 244, SEK 235, SCC 192, MEL 52.
- The 804 images with the whole clinical block missing are all non-biopsied ACK/SEK/NEV.
  Missingness alone is a label shortcut, so every result is also checked on the 1494 complete rows.

Details: `docs/eda_plan.md`. Still to do: the image-level analysis, once the images are downloaded.

## Data

PAD-UFES-20 from Mendeley Data (https://data.mendeley.com/datasets/zr7vgbcyr2). Put it in
`data/`, or on the cluster under `/vol/miltank/projects/practical_wise2627/<group>/data`.
Never commit images or metadata files: this repo is public.
