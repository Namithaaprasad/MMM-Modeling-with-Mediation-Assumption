# MMM-Modeling-with-Mediation-Assumption
Marketing Mix Modeling (MMM) with Causal Mediation
This project presents a data-driven solution to model and understand the key drivers of revenue. The objective was to build a machine learning model that explains Revenue as a function of various marketing and business levers, including paid media spend, direct response channels, pricing, and promotions. The analysis was conducted with a strong emphasis on causality and interpretability, providing actionable insights for strategic marketing decisions.

1. Data Preparation
The initial phase involved preparing the raw data for modeling. My approach was designed to handle common challenges in marketing data, ensuring the model's accuracy and robustness:
Time-Series Features: The dataset, being weekly, was enriched with features to capture both long-term trend and weekly seasonality. This ensures the model accounts for natural fluctuations and overall growth patterns.
Handling Zero-Spend Periods: A standard practice in MMM is to address the high number of zero values for some marketing channels. I applied a log transformation (log(x + 1)) to all paid media and direct response variables. This approach effectively normalizes the data, handles the zeros, and models the diminishing returns effect—the principle that the impact of ad spend decreases after a certain point.
Feature Scaling: All numerical features were scaled using a StandardScaler. This is crucial for the chosen model to prevent any single variable's magnitude from dominating the others, ensuring fair contribution from all features.
2. Modeling Approach I chose a two-stage Lasso regression model for this project. This choice was deliberate, as it combines strong predictive performance with excellent interpretability and regularization capabilities:
Lasso Regression: Lasso is a linear model that performs regularization and automatic feature selection by pushing the coefficients of less influential variables to zero. This makes the final model simpler and easier to interpret.
Validation Plan: To avoid look-ahead bias, I implemented a Time-Series Split for model validation. This ensures the model is trained on past data and evaluated on future data, providing a realistic measure of its out-of-sample performance.
3. Causal Framing
A key requirement of this project was to explicitly treat the mediator assumption that social/display media can stimulate search intent, which influences Google spend, which then affects revenue. To address this, I used a two-stage approach:
Stage 1: Social-to-Search: I first modeled Google Spend as a function of the other social media spends (Facebook, TikTok, Snapchat, Instagram).
Stage 2: Search-to-Revenue: I then built the final revenue model using all other variables, including the predicted Google Spend from the first stage.
This method provides a more nuanced and accurate representation of the marketing funnel, distinguishing between the direct effects of social spend and its indirect, mediated effects through search.

4. Diagnostics
To ensure the model's reliability and to provide actionable insights, I performed the following diagnostics:
Out-of-Sample Performance: The model was evaluated on a dedicated test set using Root Mean Squared Error (RMSE) and R-squared confirming its predictive accuracy.
Stability Checks: The use of a time-series cross-validation ensures that the model's performance is stable across different time periods.
Sensitivity Analysis: The model's coefficients were used to analyze the sensitivity of revenue to changes in key variables like Average Price and Promotions.

5. Insights & Recommendations
The final model coefficients provide a clear, quantitative understanding of the drivers of revenue. My key findings and recommendations are:
Direct Revenue Drivers: My model successfully identifies the most impactful variables, allowing for a clear interpretation of which marketing levers are most effective.
Identify Risks: The two-stage approach successfully mitigates the risk of collinearity between paid media channels, which can obscure true causal relationships.
Actionable Strategy: The insights can be used to inform marketing strategy by understanding the trade-offs between different channels (e.g., search vs. social) and optimizing budget allocation for maximum return. The model's findings are practical and defensible, providing a strong basis for a data-driven approach to growth.
