# cross-device-model-testing

Cross-vendor evaluation of machine learning models in medical imaging.  
Models are trained on data from one vendor’s device and tested on another to study robustness and generalization.

---

## Dataset

The dataset consists of medical imaging metadata and labels collected from **multiple manufacturers** (`SIEMENS`, `Planmed`, `IMS`, `IMS GIOTTO`).  
Each record contains identifiers, vendor information, image properties, and class labels.

---

## Data preprocessing and cleaning

A series of preprocessing steps were applied to prepare the dataset for training:

- **Loading optimization**  
  Dataset is loaded once into memory to avoid repeated long load times in Colab.

- **Column selection**  
  - Non-numeric columns were separated from numeric ones.  
  - Key identifiers (`study_id`, `image_id`, `Manufacturer`) were preserved.  
  - Dimension-related columns (`Rows`, `Columns`, `width`) were removed.

- **Class and feature adjustments**  
  - Overlap ratio was normalized: for healthy samples (`class = 0`) overlap was set to 0.  
  - Very small overlap values (< 0.01) were filtered out.  
  - Additional derived features (e.g., ratios) prepared the dataset for classification tasks.

- **Handling missing values**  
  - All columns with more than 2% NaN values were removed.  
  - Remaining NaNs were checked and cleaned.

- **Column reordering**  
  - A utility function was added to easily move columns into desired positions.

- **Splitting by manufacturer**  
  - DataFrames were created for each vendor (`df_SIEMENS`, `df2_Planmed`, `df3_IMS`, `df4_IMSGIOTTO`).  
  - This enables cross-vendor experiments and fair evaluation.

---

## Exploratory analysis

- **Class distribution**  
  Class balance was visualized across the dataset, showing approximately even distribution of healthy vs. affected samples.

---

## Next steps

- Validation setup (cross-vendor and within-vendor).  
- Model training and comparison.  
- Reporting metrics and visualization of results. 