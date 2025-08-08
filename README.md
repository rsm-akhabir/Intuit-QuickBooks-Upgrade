**Problem Statement**

Identify and target persuadable customers from the Wave-1 non-responder group to optimize the Wave-2 marketing upsell campaign.

**Introduction**

The Wave-1 campaign reached 801,821 business customers, but many didn’t upgrade. From a sample of 75,000, we aimed to identify those most likely to respond in Wave-2. Instead of mass emailing, we pursued a targeted approach to reduce costs, avoid customer fatigue, and boost profitability. We applied logistic regression and neural networks (with and without interaction terms and engineered features) to segment persuadable customers. Our final recommendation is based on model performance, response rates, and expected profitability.


**Exploratory Data Analysis**

* **Dataset**: 75,000 records; 22,500 held as test set
* **Data Quality**: No missing values
* **Distributions**: Purchase dollars are right-skewed; recent purchases and engagement correlate with upgrades
* **Correlations**: No major multicollinearity; tenure affects upgrade likelihood
* **Segment Insights**:

  * High-value and TurboTax users show stronger responses
  * Gender had no impact on upgrade probability
  * High spenders (4.58%) retained for strategic insight
* **Conclusion**: Focus on recent, high-value customers; use tenure and behavior for segmentation; re-engagement is critical as overall engagement declines.


**Feature Engineering**

Several new features were tested but ultimately removed due to multicollinearity or lack of predictive improvement. Examples include:

* **Avg\_Order\_Value**, **Is\_Recent\_Buyers**, **CLV**, and others
* Redundant with existing variables or added no value
* Final model retained only the most meaningful, interpretable features

**Interaction Effects**

Interaction terms were tested, especially between `bizflag` and `upgraded`, but provided no meaningful performance gain or significance. The base model without interactions was preferred.


**Modeling**

**1. Predictive Goal**: Identify non-responders from Wave-1 likely to respond in Wave-2
**2. Models Used**:

* **Logistic Regression**: Included variables like `numords`, `dollars`, `last`, `zip_bins`, `version1`, and interaction terms. AUC = 0.755
* **Neural Network (MLP)**: One hidden layer (5 neurons, tanh activation). AUC = 0.775
  **3. Evaluation**:
  
* Neural Network slightly outperformed logistic regression
* Logistic regression offered better interpretability
* Key predictors: `zip_bins`, `upgraded`, `last`; `bizflag` and `dollars` had limited impact


**Wave-2 Selection Strategy**

* Filtered Wave-1 non-responders in the test set
* Applied breakeven threshold (0.0235) using logistic regression
* Selected 5,830 high-probability businesses for Wave-2 mailing

**Expected Profit Analysis** (Neural Network model)

* **Response Rate**: 3.55%
* **Expected Buyers**: \~206
* **Cost**: \$8,220
* **Revenue**: \$12,402
* **Profit**: \$4,182
* **ROME**: 50.8%

**Key Learnings**

* **Business vs. Individual**: Similar behavior; bizflag was not significant
* **Past Upgrades Matter**: Strong predictor of future upgrade likelihood
* **Spending Alone Is Weak**: Total spend (dollars) had low correlation with upgrades


**Conclusion**

This analysis effectively identified persuadable Wave-1 non-responders using logistic regression and neural networks. The neural network model (AUC 0.775) was used to target 5,830 customers in Wave-2, yielding a projected 50.8% return on marketing spend. Prior upgrade history and recent engagement were strong predictors, while overall spending was not. This data-driven approach enables more efficient, cost-effective, and profitable customer targeting.

