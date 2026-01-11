# CSIRO – Image2Biomass Prediction

Build models that predict pasture biomass from images, ground-truth measurements, and publicly available datasets. These predictions can help farmers decide when/how to graze livestock and manage pasture recovery across seasons and regions.

---

## Problem

Given pasture images (and associated metadata), predict **five biomass components** (in grams):

- **Dry green vegetation** (excluding clover) → `Dry_Green_g`
- **Dry dead material** → `Dry_Dead_g`
- **Dry clover biomass** → `Dry_Clover_g`
- **Green dry matter (GDM)** → `GDM_g`
- **Total dry biomass** → `Dry_Total_g`

---

## Dataset

### `train.csv`
Each row corresponds to one training sample (image) and one target.

Columns:
- `sample_id` — Unique identifier for each training sample (image)
- `image_path` — Relative path to the training image (e.g., `images/ID1098771283.jpg`)
- `Sampling_Date` — Date of sample collection
- `State` — Australian state where the sample was collected
- `Species` — Pasture species present, ordered by biomass (underscore-separated)
- `Pre_GSHH_NDVI` — Normalized Difference Vegetation Index (GreenSeeker reading)
- `Height_Ave_cm` — Average pasture height (cm), measured by falling plate
- `target_name` — Biomass component (`Dry_Green_g`, `Dry_Dead_g`, `Dry_Clover_g`, `GDM_g`, `Dry_Total_g`)
- `target` — Ground-truth biomass value (grams) for the given `target_name`

### `train/`
Directory containing training images (JPEG), referenced via `image_path`.

### `test.csv`
One row per requested **(image, target)** pair.

Columns:
- `sample_id` — ID constructed from image ID and `target_name` pair
- `image_path` — Relative path to the image (e.g., `test/ID1001187975.jpg`)
- `target_name` — One of: `Dry_Green_g`, `Dry_Dead_g`, `Dry_Clover_g`, `GDM_g`, `Dry_Total_g`

Notes:
- The test set contains **800+ images**.
- The actual test images are made available to the notebook at scoring time.

### `test/`
Directory reserved for test images (hidden at scoring time); paths in `test.csv` point here.

### note:
For more information on datasets check the Kaggle Page : https://www.kaggle.com/competitions/csiro-biomass/data
---

## Submission Format

Submit a CSV in **long format** with exactly two columns:

- `sample_id` — Copy from `test.csv`; one row per requested `(image_path, target_name)` pair
- `target` — Predicted biomass value (grams) for that `sample_id` (float)

You must submit **one row per (image, target) pair**, i.e. **5 rows per test image**.

Example:
```csv
sample_id,target
ID1001187975__Dry_Green_g,0.0
ID1001187975__Dry_Dead_g,0.0
ID1001187975__Dry_Clover_g,0.0
ID1001187975__GDM_g,0.0
ID1001187975__Dry_Total_g,0.0
