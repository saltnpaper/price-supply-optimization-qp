# Joint Price & Supply Optimization: Maximizing Profit via Prescriptive Analytics

## Executive Summary
Standard inventory models (like the Newsvendor Model) often treat price as a fixed constant, optimizing only for the quantity supplied. However, this ignores a critical market reality: **pricing decisions directly influence customer demand.**

This project uses **Prescriptive Analytics** to jointly optimize both price and print quantity for a publishing company. By combining demand forecasting (Linear Regression) with advanced mathematical optimization (Quadratic Programming via Gurobi) and statistical validation (Bootstrap Simulation), the proposed model successfully identifies a strategy to increase daily profit by **1.75%**.

## Methodology & Technical Approach

### 1. Demand Modeling (Linear Regression)
* Analyzed historical price-demand data.
* Fitted a linear regression model to quantify price elasticity and determine the beta coefficients.

### 2. Joint Optimization (Quadratic Programming)
* Formulated a Non-Linear objective function to maximize Expected Profit: `Profit = E[Revenue] - E[Costs]`
* Built and solved the Quadratic Programming (QP) model using the **Gurobi Optimizer** to find the exact optimal price and order quantity while balancing disposal fees for overproduction and rush costs for underproduction.

### 3. Robustness & Stability (Bootstrap Simulation)
* Conducted Bootstrap Sampling (500+ iterations) on the original dataset to fit new beta coefficients.
* Re-ran the optimization for every iteration to build a distribution of optimal prices and quantities, ensuring the recommended strategy was statistically robust against market variance and not just a product of noise.

---

## Visualizing the Trade-off
![Joint Analysis Scatterplot](/reports/joint_tradeoff.png)

---
## Key Results & Business Impact
The optimized model recommends a strategic shift: trading a 5% price reduction for a 13% volume increase. 

| Strategy | Daily Profit | Price | Volume |
| :--- | :--- | :--- | :--- |
| **Current Model (Fixed Price Baseline)** | $231.48 | $1.00 | Baseline |
| **Proposed Model (Joint Optimization)** | **$235.54** | **$0.95** | **+13%** |
| **Improvement** | **+$4.06 (+1.75%)** | **-5%** | **+13%** |

*Business Translation:* Lowering the price to $0.95 generates sufficient additional demand to offset the lower per-unit margin, capturing an estimated **$1,481 in additional annualized profit** without increasing fixed costs.

---

## Tech Stack
* **Python** (Pandas, NumPy)
* **Optimization:** Gurobi (`gurobipy`)
* **Machine Learning / Stats:** Scikit-Learn (`LinearRegression`)
* **Data Visualization:** Seaborn, Matplotlib

## Repository Structure
* `notebooks/`: Contains the Jupyter Notebook (`newsvendor_price_optimization.ipynb`) with the complete Python code, regression models, Gurobi optimization, and bootstrap simulation.
* `reports/`: Contains the final technical report outlining the mathematical formulation and executive recommendations.

## How to Run
1. Clone the repository.
2. Ensure you have the required libraries installed: `pip install pandas numpy scikit-learn seaborn matplotlib gurobipy`.
3. **Note:** Running the optimization model requires a valid Gurobi license (academic or commercial).
