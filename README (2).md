# MS Brain MRI — Exploratory & Scientific Visualization

Exploratory data analysis and scientific visualization notebook for the **Multiple
Sclerosis (MS) brain MRI dataset** (`30393475`, 100 patients — full scans, NIfTI
volumes, registered volumes, lesion masks, GIF previews, and model-ready input).

This notebook is **EDA only** — no model training. The goal is to understand volume
geometry, intensity characteristics, and lesion burden across the cohort before any
modeling work begins.

## What's inside

The notebook (`MS_MRI_EDA_Visualization.ipynb`) walks through:

1. **Setup & Google Drive mount** — designed to run in Google Colab
2. **Archive extraction** — handles multi-part `.rar` archives
3. **File manifest** — builds a tidy table of every file per patient/modality
4. **Dataset overview** — file/patient counts per archive
5. **NIfTI metadata inspection** — shape, voxel spacing, orientation, affine sanity checks
6. **Intensity statistics** — per-patient voxel intensity distributions
7. **Multi-planar slice visualization** — axial / sagittal / coronal views
8. **Multi-patient QC montage** — quick grid view to spot registration failures or outliers
9. **Lesion mask overlays** — MRI + lesion mask visual verification
10. **Lesion volume quantification** — per-patient lesion burden (mL)
11. **Lesion connected-component analysis** — lesion count and size distribution
12. **Population-level lesion probability heatmap** — requires registered masks
13. **3D lesion surface rendering** — interactive marching-cubes mesh (Plotly)
14. **Precomputed GIF previews** — dataset-provided per-patient animated previews
15. **Correlation & statistical analysis** — relationships between summary features
16. **PCA of per-patient summary features** — cluster/outlier inspection
17. **Interactive slice explorer widget** — live slider through a chosen volume
18. **Summary dashboard** — recap of cohort-level statistics

## Requirements

Designed to run in **Google Colab** (T4 GPU runtime recommended, though not required
for EDA). If running locally, install dependencies from `requirements.txt`:

```bash
pip install -r requirements.txt
```

System dependency: `unrar` (for extracting multi-part `.rar` archives).

```bash
# Debian/Ubuntu
apt-get install unrar
```

## Data setup

This notebook expects the dataset (`30393475`, distributed as `.rar` archives) to be
available in Google Drive, shared as a folder. Update the path in the notebook's
"Path configuration" cell:

```python
DRIVE_FOLDER = "/content/drive/MyDrive/30393475"   # adjust to your Drive path
WORK_DIR     = "/content/ms_data"                   # local scratch disk for extraction
```

Data is **not included in this repository** — see `.gitignore`.

## Usage

1. Open the notebook in Google Colab.
2. Mount your Google Drive when prompted.
3. Set `DRIVE_FOLDER` to point at your copy of the dataset.
4. Run cells top to bottom. Section 5 samples 8 volumes by default for speed —
   increase this once you're ready for a full-cohort pass (expect longer runtimes
   given volume sizes and Colab RAM limits).

## Notes

- Patient IDs are inferred from filenames via regex in `guess_patient_id()` — adjust
  if your files don't follow the `0*(\d{1,4})_...` pattern.
- Section 12 (population lesion heatmap) requires masks already registered to a
  common template (the `_registered` archive).

## Author

Eram Mahamud — PhD Candidate, Deakin University
