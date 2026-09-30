# Statistical Analysis: Census Income

Capstone project for the Udacity Master's in AI program: *Conduct a Statistical Analysis Using Python*.

**Author:** Belal Nwiran

## Question

Is income level (`<=50K` or `>50K`) associated with sex in the UCI Census Income dataset?

- **H0:** Income level and sex are independent.
- **H1:** Income level and sex are not independent.

## Dataset

- **Name:** Census Income (also called "Adult")
- **Source:** UCI Machine Learning Repository, https://archive.ics.uci.edu/dataset/20/census+income
- **File used:** `adult.data` (original file, unchanged)
- **Size:** 32,561 rows and 15 columns. After removing 24 exact duplicate rows, 32,537 rows remain.
- **Note:** the file has no header row, so the notebook assigns the column names when loading it.

## What is in this repository

| File | Description |
|---|---|
| `analysis.ipynb` | Jupyter notebook: loading, cleaning, descriptive statistics, three visualizations, chi-square test, summary |
| `Statistical_Analysis_Report.pdf` | Written report for technical and non-technical readers, with citations and references |
| `adult.data` | Original dataset file |
| `requirements.txt` | Python packages, created with `pip freeze > requirements.txt` |
| `README.md` | This file |

## How to run

1. Create and activate a virtual environment (optional but recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   ```

2. Install the packages:

   ```bash
   pip install -r requirements.txt
   ```

3. Start Jupyter and open the notebook:

   ```bash
   jupyter lab
   ```

4. Keep `adult.data` in the same folder as `analysis.ipynb`, then choose **Restart Kernel and Run All Cells**.

The notebook was developed with Python 3.13 and pandas 3. The code uses pandas 3 behavior (for example `describe(include="str")`), so install the versions in `requirements.txt`.

## Method in brief

1. **Load and check the data:** column names, data types, missing values, duplicates.
2. **Clean:** remove 24 exact duplicate rows. Keep the rows with the maximum capital gain (99,999), because they are all in the `>50K` group and removing them would change the counts being tested.
3. **Describe the data:** summary statistics, category counts, skewness, and the share of zeros in the capital columns.
4. **Visualize:** a bar chart of the `>50K` share by sex, a boxplot of weekly hours by income group and sex, and a correlation heatmap of the numeric columns.
5. **Test:** a chi-square test of independence with Cramér's V as the effect size. The notebook checks the expected-count assumption.

## Main results

- 11.0% of women and 30.6% of men in the data earn more than 50K.
- Chi-square test: χ²(1, N = 32,537) = 1517.61, p < .001.
- Cramér's V = 0.22, between the small and medium benchmarks for one degree of freedom.
- This is an association in one sample. It does not show that sex causes the difference, and the test does not control for other factors such as age, hours, or occupation.

## Limitations

- Observational data, and only two variables are tested.
- Missing values in `workclass`, `occupation`, and `native_country` (none in the tested variables).
- 159 rows have the maximum capital gain value of 99,999, which the dataset documentation does not explain.
- The census sampling weight (`fnlwgt`) is not used, so results describe this sample and not necessarily all adults.
- The sample is not balanced by sex, and most people in it are White.

See the report for the full discussion.

## References

- Kim, H.-Y. (2017). Statistical notes for clinical researchers: Chi-squared test and Fisher's exact test. *Restorative Dentistry & Endodontics, 42*(2), 152–155. https://doi.org/10.5395/rde.2017.42.2.152
- Lusa, L., Proust-Lima, C., Schmidt, C. O., Lee, K. J., le Cessie, S., Baillie, M., Lawrence, F., Huebner, M., & on behalf of TG3 of the STRATOS Initiative. (2024). Initial data analysis for longitudinal studies to build a solid foundation for reproducible analysis. *PLOS ONE, 19*(5), Article e0295726. https://doi.org/10.1371/journal.pone.0295726
- Sullivan, G. M., & Feinn, R. (2012). Using effect size—or why the P value is not enough. *Journal of Graduate Medical Education, 4*(3), 279–282. https://doi.org/10.4300/JGME-D-12-00156.1

## AI assistance

Claude (Anthropic) was used as a planning and review assistant for this project, including help with dataset selection, checking results against the rubric, and drafting text. The analysis was run and the outputs were produced by the author.