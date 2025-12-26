# Customer Survival Analysis & Churn Prediction

Customer churn — also called attrition or defection — refers to clients leaving a service. Telecom, internet, TV, insurance, and monitoring companies track churn closely, as retaining an existing customer is far cheaper than acquiring a new one. Predictive models help identify likely defectors, enabling targeted retention strategies.

This project focuses on performing **customer survival analysis** and building a **churn prediction model**. Additionally, a web app has been created to analyze why a customer may leave and estimate their **expected lifetime value**.

---

## Final Customer Churn Prediction App

<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/app-pic.png" alt="Final App" width="600">

---

## Project Structure

```
.
├── Images/                             : project images
├── static/                             : plots for gauge charts, survival curves, SHAP values
│   └── images/
│       ├── hazard.png
│       ├── surv.png
│       ├── shap.png
│       └── new_plot.png
├── templates/                          : HTML templates for Flask app
│   └── index.html
├── Customer Survival Analysis.ipynb    : Kaplan-Meier curves, log-rank tests, Cox proportional hazard model
├── Exploratory Data Analysis.ipynb     : Data analysis and visualization
├── Churn Prediction Model.ipynb        : Random Forest churn prediction model
├── app.py                              : Flask application
├── app-pic.png                         : Screenshot of final app
├── explainer.bz2                       : SHAP explainer
├── model.pkl                           : Random Forest model
├── survivemodel.pkl                    : Cox proportional hazard model
├── requirements.txt                    : Python dependencies
├── Procfile                            : Deployment configuration
└── README.md                            : Project overview
```

---

## Customer Survival Analysis

**Survival Analysis:**
A set of statistical methods to examine time-to-event data — in this case, how long a customer stays with a service. Events can range from churn to other types of outcomes.

**Goals:**

* Understand how churn likelihood changes over time
* Model relationships between churn, time, and customer attributes
* Identify key factors driving churn
* Estimate survival curves and hazard rates for individual customers
* Calculate customer lifetime value (CLV)

**Kaplan-Meier Survival Curve:**

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/SurvivalCurve.png" width="400" height="300">
</p>

Observations:

* Churn remains relatively low initially; after ~60 months, it increases noticeably
* Survival probability steadily decreases between 3–60 months

**Log-Rank Test:**
Evaluates whether survival distributions differ significantly between customer groups.

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/gender.png" width="250">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/Senior%20Citizen.png" width="250">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/partner_1.png" width="250">
</p>

Key insights:

* Gender and phone service type are not significant predictors of churn
* Customers with families and younger ages tend to stay longer
* Lack of additional services (online backup, streaming, etc.) increases churn risk
* Month-to-month contracts and non-automatic payments correlate with higher churn

---

## Survival Regression

Using the **Cox proportional hazards model**, we quantify the impact of multiple risk factors on customer churn.

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/Survival-analysis.png" width="750">
</p>

* Enables prediction of survival and hazard curves for individual customers
* Supports calculation of **expected customer lifetime value**

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/survival.png" width="400">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/hazard.png" width="400">
</p>

---

## Customer Churn Prediction

**Analysis:**

* Higher tenure correlates with lower churn
* New customers without extra services are more likely to leave
* Fiber-optic Internet and month-to-month contracts contribute to higher churn

**Modelling Approach:**

* **Random Forest classifier** to handle non-linear features
* Addressed **class imbalance** (1:3 ratio) with weighted classes
* Hyperparameters optimized via **Grid Search CV**
* Model performance: **F1 score 0.62, ROC-AUC 0.85**

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/model_1.png" width="600">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/model_feat_imp.png" width="600">
</p>

---

## Explainability

**SHAP, Permutation Importance, Partial Dependence Plots** allow interpretation of feature contributions to churn predictions.

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/eli51.png" width="200">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/eli52.png" width="200">
</p>

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/pdp_tenure.png" width="400">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/pdp_contract.png" width="400">
</p>

<p align="center">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/pdp_monthly_charges.png" width="400">
<img src="https://github.com/Sanulajr/Customer-Survival-Analysis-And-Churn-Prediction-Master/blob/main/Images/pdp_total_charges.png" width="400">
</p>

---

## Flask Web App

* **Random Forest model** deployed via Flask
* SHAP explainers visualized in the app
* Survival and hazard curves from Cox model included
* Provides **churn probability, severity gauge, and feature explanations**

