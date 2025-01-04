# Gaussian Process Regression for Option Pricing

## **Meta-Comment**
This project focused on applying Gaussian Process Regression (GPR) to improve option pricing by modeling the errors of the Black-Scholes (BS) model. The primary goal was to gain practical experience with GPR in a financial context. The BS model, commonly used for pricing options, often deviates from actual market prices due to its simplifying assumptions. By fitting the residuals (differences between market prices and BS predictions) using GPR, the objective was to capture patterns in the errors and enhance the accuracy of BS predictions.

# European vs. American Options: What’s the Difference?

The Black-Scholes model was designed for European options, which can only be exercised at their expiration date. In contrast, the options analyzed in this project were American-style options, which can be exercised at any time before expiration. This flexibility introduces an important factor: dividends.

Holders of American options often exercise them just before dividend dates to receive the dividend payout. This behavior creates a need for pricing models that account for early exercise and dividends—something the Cox model handles well, but the standard BS model does not.

# The Discrepancy: Why Did It Happen?

The implied volatilities provided by WRDS were likely derived using models that correctly account for dividends, such as the Cox model or a dividend-adjusted BS model. However, in this project, these implied volatilities were reused in a plain BS model, which ignores dividends. As a result, the BS model systematically underpriced options near dividend dates.

This discrepancy was revealed by analyzing the residuals and prompted further investigation. Although the conclusion—that missing dividend adjustments caused the error—is straightforward, the project was valuable as a methodological exercise and provided meaningful hands-on experience with GPR.

---

## **Project Overview**

The project involved analyzing data for **three Apple options** with different maturities and using **Gaussian Process Regression (GPR)** to improve BS predictions by fitting residuals between the market prices and BS-predicted prices.

### **Methodology**

1. **Data and Preprocessing**:
   - Data for three Apple options was obtained from WRDS.
   - Options were selected based on high trading volume to ensure liquidity and availability of implied volatilities.

2. **Residual Modeling**:
   - BS prices were computed using the implied volatilities provided in the dataset.
   - Residuals were calculated as:
     \[
     \text{Residuals} = \text{Market Price} - \text{BS Price}
     \]
   - These residuals were fitted using GPR to capture patterns and improve pricing predictions.

3. **Splitting Strategy**:
   - The data was split based on **time to maturity**:
     - **Training set**: Options with time to maturity \( T > 0.3 \) years.
     - **Validation set**: Options with \( 0.1 < T \leq 0.3 \) years.
   - This split ensured that the model was trained only on past data, making the methodology robust by avoiding **future information leakage**.
   - The validation set focused on near-expiration options, where pricing errors tend to be more pronounced.

4. **Gaussian Process Regression**:
   - Various kernels were used (e.g., RBF, Matern) to fit the residuals.
   - Hyperparameter tuning was performed using **RandomizedSearchCV** with a predefined split.
   - The corrected option prices were obtained by adding the GPR-predicted residuals to the original BS prices.

---

## **Files in the Repository**

- **`Final_Project_Code.ipynb`**: The main Jupyter notebook containing the project code and methodology.
- **`Proposal.pdf`**: The input task and requirements provided for the project.
- **`CEE5735_Final_Project.pdf`**: The final report, documenting the methodology, analysis, and conclusions. *(The report is well-written and provides a detailed explanation of the project.)*
- **`gp_hyperparameters_summary.csv`**: A summary of the hyperparameter tuning results for GPR.
- **`Git_History_Cleanup_Log.pdf`**: A log documenting the process of cleaning the Git history to remove large files I had committed by mistake.

---

## **Disclaimer**

- The data used in this project was obtained from **Wharton Research Data Services (WRDS)** and cannot be shared publicly due to licensing policies.
- This README focuses on describing the methodology and findings without providing data.

---

## **Acknowledgments**

This project was conducted as part of the **CEE5735: Mathematical Modeling of Natural and Engineered Systems** course at Cornell University. Special thanks to the course instructors for their guidance.
