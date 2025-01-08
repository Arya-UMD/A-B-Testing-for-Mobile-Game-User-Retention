# **A/B Testing for Mobile Game User Retention**

**Dataset Link**: [Kaggle Dataset](https://www.kaggle.com/datasets/yufengsui/mobile-games-ab-testing)  

---

## **Project Overview**  
This project aimed to analyze the effect of two game versions (“gate_30” and “gate_40”) on user engagement and retention using a dataset of 90,189 records. An A/B test was conducted to evaluate key metrics such as the number of game rounds played and retention rates after 1 and 7 days.

---

## **1. Data Preparation and Cleaning**  
- **Dataset Size:** 90,189 records  
- **Tools Used:** PySpark, Pandas  
- **Steps Taken:**
  - Dropped missing values and duplicates.
  - Converted the cleaned Spark DataFrame to Pandas for detailed analysis.
  
---

## **2. Exploratory Data Analysis (EDA)**  

- **Key Metrics:**
  - **Sum of Game Rounds Played:** Average number of game rounds users played.
  - **Retention Rate:** Percentage of users returning after 1 and 7 days.

**Additional Analyses:**

1. **Quantile-Quantile (Q-Q) Plots:**
   - Used Q-Q plots to check for the normality of the "sum_gamerounds" distribution.
   - The plots revealed deviations from the diagonal line, indicating that the game rounds data are not perfectly normally distributed, though close enough for the use of t-tests.

2. **Bootstrapping Means:**
   - Bootstrapping was performed to calculate mean estimates by generating 1,000 random samples (with replacement) from the game rounds data.
   - The bootstrapped distributions of the means for both versions ("gate_30" and "gate_40") were plotted to check for potential bias.
   - Results showed consistent and unbiased mean estimates across multiple resampling iterations, validating the reliability of the sample mean comparisons.

**Visualizations:**  

- Bar plots showing the average number of game rounds for each version:
  ![image](https://github.com/user-attachments/assets/27f66bec-dc45-4cca-8dcc-85ea9f5e1950)  

- Q-Q plots for checking normality:
  ![image](https://github.com/user-attachments/assets/qq_plot_gate30)  
  ![image](https://github.com/user-attachments/assets/qq_plot_gate40)  

- Bootstrapped means histograms:
  ![image](https://github.com/user-attachments/assets/bootstrap_gate30)  
  ![image](https://github.com/user-attachments/assets/bootstrap_gate40)  

- Retention rates visualized for both 1-day and 7-day intervals:
  ![image](https://github.com/user-attachments/assets/bd9cd65c-9cb5-4aef-bac2-b85deaa963cd)  
  ![image](https://github.com/user-attachments/assets/55e596eb-319d-4a9a-8f22-7582c21b2fb3)  

---

## **3. Statistical Analysis and Hypothesis Testing**  
- **Statistical Test Used:** Two-sample t-test  
- **Null Hypothesis (H₀):** There is no significant difference between the two versions for a given metric.  
- **Alternative Hypothesis (H₁):** There is a significant difference between the two versions for a given metric.  

**Results:**

| Metric              | p-value               | Conclusion                          |
|---------------------|-----------------------|-------------------------------------|
| Game Rounds Played  | 0.376                  | No significant difference           |
| 1-Day Retention     | 0.074                  | No significant difference           |
| 7-Day Retention     | 0.0016                 | Significant difference (p < 0.05)   |

- **Interpretation:** The "gate_30" version had a significantly better 7-day retention rate than "gate_40", with a p-value < 0.05.

---

## **4. Conclusions and Recommendations**  
- **Findings:**
  - There was no notable difference in the immediate engagement (game rounds played).
  - Users retained better after 7 days when the gate was placed at level 30, indicating that the progression point at level 40 may be too challenging.
  
- **Recommendations:**
  1. Maintain the gate at level 30 or experiment with intermediate gate levels.
  2. Conduct qualitative user feedback to understand the drop-off reasons at level 40.
  3. Explore changes to in-game incentives or difficulty tuning for level 40 to improve long-term retention.

---

## **Technologies and Methods Used**  
- **Data Processing:** PySpark (for large-scale data handling), Pandas  
- **Visualization:** Matplotlib, Seaborn  
- **Statistical Testing:** SciPy (t-tests), Statsmodels  
- **Framework:** Jupyter Notebooks / Colab for interactive development  
