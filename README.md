This Jupyter notebook explores which job and workplace characteristics are associated with salary, then tests those relationships statistically. It includes exploratory charts, group comparisons, correlation tests, and a multiple linear regression with assumption checks.

## Dataset

The notebook expects `job_salary_prediction_dataset.csv`, a 250,000-row dataset with 10 columns:

| Column | Type | Description |
| --- | --- | --- |
| `salary` | Numeric | Salary outcome being analyzed |
| `experience_years` | Numeric | Years of experience |
| `skills_count` | Numeric | Number of skills |
| `certifications` | Numeric | Number of certifications |
| `job_title` | Category | Role or job title |
| `education_level` | Category | Highest education level |
| `industry` | Category | Industry |
| `company_size` | Category | Employer size |
| `location` | Category | Country or location grouping |
| `remote_work` | Category | On-site, hybrid, or remote status |

The saved notebook output reports no missing values and no duplicate rows. The CSV itself is not included with this README; obtain it separately before running the notebook.

## Notebook sections

1. **Data inspection:** previews, data types, summary statistics, missing values, and duplicate count.
2. **Exploratory analysis:** salary distributions; numeric and categorical relationships; combined-category heatmaps; and outlier checks using the IQR rule.
3. **Hypothesis tests:** Pearson and Spearman correlations for numeric features, Kruskal–Wallis group comparisons for categorical features, and a multiple OLS model.
4. **Model diagnostics and ranking:** overall model fit, Type II ANOVA for whole-feature tests, residual checks, multicollinearity checks for numeric predictors, and a feature-importance summary.

## Main findings in the saved notebook

- Salary is mildly right-skewed. The saved output reports a mean of about 145,718 and a median of about 143,453.
- Experience has the strongest numeric correlation with salary in the pairwise analysis (`r` ≈ 0.438). Skills count and certifications have weaker positive correlations.
- Salary varies substantially by job title, education, company size, and location. Industry shows little difference in the saved group test.
- The OLS model reports an R-squared of about 0.963. In its Type II ANOVA output, location, experience, company size, job title, and education have the largest partial eta-squared values; industry is not significant in that adjusted model.
- The IQR check flags about 0.93% of salary observations as outliers and no experience observations. These are flags for review, not automatic data errors.

The dataset appears unusually balanced across several input categories. Treat these findings as descriptions of this dataset, not evidence that the same salary relationships hold in the broader labor market. With 250,000 rows, very small differences can also produce tiny p-values; consider effect sizes and uncertainty alongside statistical significance.

## Requirements

- Python 3
- Jupyter Notebook or JupyterLab
- `pandas`, `matplotlib`, `seaborn`, `scipy`, and `statsmodels`

Install the packages with:

```bash
pip install pandas matplotlib seaborn scipy statsmodels jupyter
```

## Run the notebook

1. Place `job_salary_hypothesis_testing_assignment.ipynb` and `job_salary_prediction_dataset.csv` in the same folder.
2. In the first code cell, use a relative path so the notebook works on another computer:

   ```python
   job_salary = pd.read_csv("job_salary_prediction_dataset.csv")
   ```

3. If running all cells in a fresh kernel, add this import before the remote-work Kruskal–Wallis test, which references `stats.kruskal`:

   ```python
   from scipy import stats
   ```

4. Run the notebook from top to bottom.

## Interpretation and reproducibility notes

- The Kruskal–Wallis test assesses differences in group distributions/ranks; it does not directly test equality of means. Some notebook hypothesis statements describe mean differences, so align the wording with the test or choose a mean-based test after checking its assumptions.
- The saved ranking narrative conflicts with the fitted model's Type II ANOVA output. Use the computed ANOVA table when describing adjusted feature effects, and update the narrative to match it.
- Re-run the notebook after changing the data path or imports. Saved outputs may reflect an earlier kernel state and do not guarantee every cell runs from a clean kernel.
- The OLS model is explanatory. Its high in-sample R-squared alone does not establish out-of-sample predictive performance or causal effects.
