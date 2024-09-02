# Model Files

This directory should contain the trained machine learning models.

## Expected Files
- `model.joblib` - The trained LightGBM model in joblib format
- `model.pkl` - The trained model in pickle format (backup)

## How to Get Models
1. Train the model by running the Jupyter notebook `ad_click_prediction.ipynb`
2. The trained models will be saved automatically in this directory
3. Alternatively, download pre-trained models from the project releases (if available)

## Model Information
- **Model Type**: LightGBM Classifier
- **Task**: Binary classification for ad click prediction
- **Input Features**: region_id, city_id, tags_cont, tags_bhv, rubrica, rate, ctr_sort, rv_perc, slider
- **Target**: Binary (0 = no click, 1 = click)

## Note
Model files are excluded from git due to their large size. Use Git LFS if you need to version control model files.
