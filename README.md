# TexTune – Production Order Delay Risk Prediction
 
## Files
| File | Purpose |
|---|---|
| `TexTune.ipynb` | Full analysis: data checks, EDA, modelling, evaluation, planner recommendation, bonus, assumptions |
| `textune_production_orders.csv` | Input data (must stay next to the notebook) |
| `top_20_at_risk_orders.csv` | Output: `order_id`, `predicted_delay_probability`, `predicted_class` for the 20 highest-risk orders |
| `TexTune_Summary.pdf` | One-page summary |
| `AI_USAGE.md` | AI usage statement |
| `requirements.txt` | Python libraries |
 
## How to run
1. Use Python 3.10 or newer.
2. Install the libraries (CatBoost is needed in addition to the usual ones):
```bash
pip install -r requirements.txt
```
3. Keep `textune_production_orders.csv` in the same folder as the notebook.
4. Open the notebook and choose **Kernel → Restart & Run All**:
```bash
jupyter notebook TexTune.ipynb
```
 
5. It takes about a minute or two and rewrites `top_20_at_risk_orders.csv`.

## Approach in brief
- Missing numbers are filled with the training median inside the model pipeline (plus a "was missing" flag); `order_id` and the start date are not model inputs.
- Stratified 80/20 split. Four models: Logistic Regression (baseline), Weighted Logistic Regression, Random Forest and CatBoost. No SMOTE and no PCA.
- Metrics: accuracy, precision, recall, F1, classification report and confusion matrices. The cutoff for "delayed" is chosen by best F1 on out-of-fold training predictions.
- The top-20 list uses 5-fold out-of-fold probabilities, so no order is scored by a model that saw it.
 