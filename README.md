# ⚡ Energy Consumption Prediction with Linear & Ridge Regression

## 📌 Project Overview
In this project, I built a **Linear Regression model** to predict **Energy Consumption** based on multiple real-world features such as area, occupants, appliances, and temperature.

Initially, the model produced **almost perfect results** on the test set:

- **R² ≈ 0.999999**
- **MSE ≈ 0.00018**

At first glance, this raised a serious question:

> ❓ *Is my model overfitting or leaking data?*

This repository documents the **full investigation**, validation, and improvement of the model using **L2 regularization (Ridge Regression)**.

---

## 🧠 Step 1: Suspecting Overfitting
Such a high R² score is rare in real-world datasets.  
So the first concern was:
- Overfitting?
- Data leakage?
- Evaluation on training data?

To verify this, I carefully reviewed:
- Train–test split logic
- Preprocessing steps
- Feature–target separation
- Evaluation methodology

✔ The model was evaluated **only on test data**  
✔ No data leakage was found  
✔ Preprocessing was done correctly  

This confirmed that the high performance was due to the **dataset being highly linear and low-noise**, not due to a mistake.

---

## 🔬 Step 2: Applying L2 Regularization (Ridge Regression)
Even though the model generalized well, I applied **L2 regularization** as a best practice to:

- Control coefficient magnitude
- Improve numerical stability
- Demonstrate bias–variance tradeoff
- Make the model more robust

The Ridge Regression loss function becomes:

\[
J = \text{MSE} + \alpha \sum w^2
\]

---

## 📊 Step 3: Tuning Alpha (Regularization Strength)
I trained Ridge Regression models using multiple values of **alpha (α)** and evaluated performance using **R² score on test data**.

### Results:

| Alpha (α) | R² Score |
|----------|---------|
| 0.0001 | 0.9999999998 |
| 0.001  | 0.9999999998 |
| 0.01   | 0.9999999993 |
| 0.1    | 0.9999999585 |
| 1      | 0.9999959261 |
| 10     | 0.9996141857 |
| 100    | 0.9752740071 |

---

## 📈 Observations
- **Small α** behaves like standard Linear Regression
- **Moderate α (0.1 – 1)** provides healthy regularization with minimal performance loss
- **Large α (100)** introduces high bias and leads to underfitting

This clearly demonstrates the **bias–variance tradeoff**.

---

## ✅ Final Conclusion
- The original Linear Regression model was **not overfitting**
- The dataset is **synthetic / highly linear with minimal noise**
- L2 regularization confirms model stability
- Ridge Regression helps control coefficients without sacrificing accuracy

> High accuracy alone does not imply overfitting —  
> validation, reasoning, and regularization matter.

---

## 🛠️ Technologies Used
- Python
- NumPy
- Pandas
- Scikit-learn
- Matplotlib

---

## 🚀 Key Learning
This project reinforced an important ML lesson:

> **Always question unusually good results, validate your pipeline, and use regularization to ensure robustness.**

---

## 📂 Repository Structure
├── energy_data.csv
├── energy_data_prediction_Linear_regression.ipynb
├── README.md
├── requirements.txt


---

## 🔗 Future Improvements
- Add noise to data and re-evaluate
- Compare Ridge vs Lasso vs ElasticNet
- Visualize coefficient shrinkage
- Apply cross-validation for alpha selection
