# EDA summary (first pass over metadata.csv)

## Structure

- images: 2298
- patients: 1373
- lesion_ids_raw: 1641
- lesions_patient_lesion_key: 1891
- lesions_with_multiple_images: 361
- images_in_multi_image_lesions: 768
- patients_with_multiple_lesions: 355
- patients_with_multiple_diagnoses: 179

`lesion_id` is only unique within a patient; group splits by `patient_id`.

## Labels and ground truth

| diagnostic   |   False |   True |   biopsied_frac |
|:-------------|--------:|-------:|----------------:|
| ACK          |     552 |    178 |       0.243836  |
| BCC          |       0 |    845 |       1         |
| MEL          |       0 |     52 |       1         |
| NEV          |     184 |     60 |       0.245902  |
| SCC          |       0 |    192 |       1         |
| SEK          |     220 |     15 |       0.0638298 |

## Clinical block missingness by class and biopsy

| diagnostic   |   block_missing=False/biopsied=False |   block_missing=False/biopsied=True |   block_missing=True/biopsied=False |
|:-------------|-------------------------------------:|------------------------------------:|------------------------------------:|
| ACK          |                                  105 |                                 178 |                                 447 |
| BCC          |                                    0 |                                 845 |                                   0 |
| MEL          |                                    0 |                                  52 |                                   0 |
| NEV          |                                   15 |                                  60 |                                 169 |
| SCC          |                                    0 |                                 192 |                                   0 |
| SEK          |                                   32 |                                  15 |                                 188 |

The 804 rows with the clinical block missing are all non-biopsied ACK/SEK/NEV: missingness alone separates malignant from non-malignant classes. Run the main experiments with and without missingness indicators and on complete rows only.

## Metadata informativeness (association with diagnosis)

| attribute           |   cramers_v_all |   cramers_v_complete_rows |
|:--------------------|----------------:|--------------------------:|
| smoke               |           0.505 |                     0.14  |
| has_sewage_system   |           0.503 |                     0.095 |
| has_piped_water     |           0.503 |                     0.091 |
| pesticide           |           0.502 |                     0.145 |
| skin_cancer_history |           0.502 |                     0.083 |
| gender              |           0.501 |                     0.09  |
| drink               |           0.5   |                     0.055 |
| cancer_history      |           0.499 |                     0.038 |
| age                 |           0.456 |                   nan     |
| grew                |           0.431 |                     0.351 |
| itch                |           0.378 |                     0.305 |
| changed             |           0.377 |                     0.331 |
| elevation           |           0.376 |                     0.316 |
| bleed               |           0.356 |                     0.284 |
| fitspatrick         |           0.325 |                     0.133 |
| background_father   |           0.316 |                     0.131 |
| background_mother   |           0.311 |                     0.118 |
| region              |           0.293 |                     0.278 |
| hurt                |           0.285 |                     0.239 |
| diameter_2          |           0.175 |                   nan     |
| diameter_1          |           0.167 |                   nan     |

## Metadata-only baselines (5-fold patient-grouped CV)

| setting                 | model   |    n |   bacc_mean |   bacc_std |   macro_auc_mean |   macro_auc_std |
|:------------------------|:--------|-----:|------------:|-----------:|-----------------:|----------------:|
| full+indicators         | logreg  | 2298 |       0.654 |      0.035 |            0.911 |           0.006 |
| full+indicators         | rf      | 2298 |       0.513 |      0.028 |            0.903 |           0.011 |
| full,no indicators      | logreg  | 2298 |       0.654 |      0.035 |            0.911 |           0.006 |
| full,no indicators      | rf      | 2298 |       0.521 |      0.032 |            0.904 |           0.009 |
| full,complete rows only | logreg  | 1494 |       0.57  |      0.048 |            0.835 |           0.019 |
| full,complete rows only | rf      | 1494 |       0.372 |      0.025 |            0.84  |           0.021 |
| demographic             | logreg  | 2298 |       0.506 |      0.035 |            0.825 |           0.011 |
| demographic             | rf      | 2298 |       0.398 |      0.031 |            0.777 |           0.031 |
| symptoms                | logreg  | 2298 |       0.57  |      0.038 |            0.883 |           0.004 |
| symptoms                | rf      | 2298 |       0.492 |      0.04  |            0.865 |           0.01  |
| history                 | logreg  | 2298 |       0.341 |      0.05  |            0.74  |           0.012 |
| history                 | rf      | 2298 |       0.294 |      0.047 |            0.694 |           0.034 |

## Fold table (committed split)

|   fold |   ACK |   BCC |   MEL |   NEV |   SCC |   SEK |   images |   patients |
|-------:|------:|------:|------:|------:|------:|------:|---------:|-----------:|
|      0 |   146 |   169 |    11 |    49 |    38 |    47 |      460 |        275 |
|      1 |   146 |   169 |    10 |    49 |    39 |    47 |      460 |        273 |
|      2 |   146 |   169 |    10 |    49 |    38 |    47 |      459 |        276 |
|      3 |   146 |   169 |    11 |    49 |    38 |    47 |      460 |        276 |
|      4 |   146 |   169 |    10 |    48 |    39 |    47 |      459 |        273 |

## Images

- image directory not found; image statistics skipped
