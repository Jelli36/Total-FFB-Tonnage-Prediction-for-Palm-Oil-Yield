# Total-FFB-Tonnage-Prediction-for-Palm-Oil-Yield

Predicting quantity of FFB (in tons): Machine Learning Process and Insights

## Introduction:
This research aims to develop a machine-learning model capable of predicting Total FFB Tonnage, a key measure of oil palm yield, using a comprehensive dataset of plantation records. Various factors, including geographical coordinates, plantation characteristics, environmental conditions, and historical weather data, inform the yield prediction. By identifying the most influential features, this study aims to enhance our understanding of the factors affecting oil palm productivity and provide actionable insights for optimizing agricultural practices.

## Data Preparation:
The dataset included key attributes:
### Plantation, Division, Field: 
Hierarchical identifiers for the plantations, divisions, and fields (where data was collected)
### long_appox, lat_appox: 
Geographical coordinates that could influence the yield due to regional climate variations.
### masl: 
Elevation in meters above sea level, which impacts climate and soil conditions
### Date_Planting: 
Planting data, which may influence yield through crop maturity.
### Year, Month: 
Seasonal effects and yearly trends affecting yield.
### Rainfall: 
The rainfall received, measured in millimeters (mm).
### Temperature lags: 
Historical minimum and maximum temperatures lagged over time, reflecting climate conditions before the current period.
### Hectrage: 
The total area of land measured in hectares.
### Timespan: 
The duration or interval over which the data was collected or analyzed.
### Yield_tha: 
The agricultural yield per unit area, typically measured in tons per hectare.
## The following steps were taken to prepare the data for modeling:
Feature Engineering: The ‘Field’, ‘Plantation’, ’Division’, and ‘Date_Planting’ columns were divided into two new fields: field, plantation, division, and year_planted.

### Dropped Columns: 
The following columns were dropped as it is no longer relevant in predicting the Total FFB Tonnage: ‘Field’, ‘Plantation’, ’Division’,  ‘Date_Planting’,  ‘Month’, ’Year_month’, ’start’, ’end’, ‘ann.start’, and ‘ann.end’.

### Correlation Matrix: 
A correlation matrix was made to determine which columns have a high correlation. Columns with a correlation of 0.7 and higher or -0.7 or lower are dropped to avoid overfitting and multicollinearity of the data. Multicollinearity can cause the standard error to become inflated, making it hard to interpret the model’s output meaningfully.

### Categorical Encoding: 
‘field’, ‘plantation’, and ‘division’ are categorical variables; the function ‘pd.get_dummies’ will create a separate binary column for each unique category within these columns. After that, the columns ‘field’, ‘plantation’, and ‘division’ are dropped.

### Scaler: 
Use StandardScaler() for all features and the target. It is to ensure that the data points have a balanced scale. The features in the dataset have different units or ranges, which can affect the performance of the models. Scaling ensures that all features contribute equally to the model.

### Train-Test Split:
The dataset was split into training and testing sets (80-20 split) to evaluate model performance.

## Modeling Approach:
I chose Random Forest Regression, XGBoost, and LightGBM as the models to predict the Total FFB Tonnage. Random Forest is a robust model for structured data and provides good performance. XGBoost and LightGBM were also chosen due to their efficiency and ability to handle complex data relationships. To ensure consistency, hyperparameter tuning was conducted for Random Forest, XGBoost, and LightGBM with ‘n_estimators = 200’ and ‘random_state = 42’.


## Model Performance:
After training the Random Forest model, I evaluated its performance using five main metrics:
## Mean Squared Error  (MSE): 
### Random Forest:
The Random Forest model has an MSE of 0.0144, indicating that the model is making relatively low prediction errors on average. Although not the best compared to other models, the error is still small, suggesting that Random Forest performs well.
### XGBoost: 
XGBoost has a slightly lower MSE of 0.0105, meaning it has smaller prediction errors on average than Random Forest. This suggests that XGBoost is performing better in terms of prediction accuracy.
### LightGBM: 
LightGBM achieves the lowest MSE of 0.0097, indicating the smallest prediction errors on average among the three models. This suggests that LightGBM is the most accurate model for minimizing prediction error.

## R-squared (R²): 
### Random Forest:
The R² value of 0.9747 shows that Random Forest explains 97.47% of the variance in the target variable. This indicates a strong fit to the data and that the model captures most underlying patterns.

### XGBoost: 
With an R² value of 0.9816, XGBoost explains 98.16% of the variance in the target variable. This is a very strong result, indicating that the model fits the data well and captures almost all the important patterns.

### LightGBM: 
The R² value of 0.9831 shows that LightGBM explains 98.31% of the variance in the data. This is slightly better than XGBoost, which indicates that LightGBM fits the data slightly better and captures more of the data's variance.


## Mean Absolute Error (MAE): 
The Mean Absolute Error (MAE) is 0.0705, which provides another measure of the average magnitude of errors in the predictions. While MAE doesn’t give as much weight to large errors as MSE, the value suggests that the models generally make average prediction errors in the range of 0.0705 units. This is a relatively small error, suggesting overall good model performance.


## Root Mean Squared Error (RMSE):  
The Root Mean Squared Error (RMSE) is 0.0983, indicating that, on average, the models' predictions deviate from the true values by approximately 0.0983 units. Since RMSE gives more weight to larger errors, this is a relatively low value, confirming that the models generally make accurate predictions.


## Cross-validation (CV): 
The Cross-validation MSE is 0.0422, which represents the average MSE across multiple data splits during cross-validation. This value suggests that the models are generalizing well and not overfitting to the training data, as the cross-validation error is relatively low. It confirms that the models are likely to perform well on unseen data.

## Visual Analysis:

### Chart 1. Actual vs Predicted
The scatter plot comparing actual and predicted rating scores indicates that the model performs well overall, as most points align closely with the red dashed line representing ideal predictions (y = x). However, some deviations are noticeable, particularly at the lower and higher ends of the rating scale, suggesting the model is less accurate with extreme values. The dense clustering around the mid-range ratings shows that the model effectively captures general trends but has difficulty handling outliers or less frequent values. These observations suggest that further optimization may be needed to enhance accuracy across the rating spectrum.

### Chart 2. Relationship Between Hectrage and Total FFB Tonnage
The scatter plot examining the relationship between hectarage and total FFB tonnage reveals a positive correlation, with the data points generally following the upward trend indicated by the red regression line. This suggests that larger hectarage is associated with higher FFB tonnage. However, there is noticeable variability around the line, particularly for mid-sized hectares (50–100 hectares), where the FFB tonnage values are widely dispersed. The spread indicates that factors other than hectarage may influence FFB tonnage, leading to inconsistencies in the predictions. While the model captures the overall trend well, refining it to account for this variability could improve predictive accuracy for specific hectarage ranges.



## Conclusion:

This project successfully developed machine learning models to predict the Total FFB Tonnage, an essential metric for oil palm yield prediction, using a dataset of plantation records. The models, including Random Forest, XGBoost, and LightGBM, demonstrated strong predictive performance across key metrics such as Mean Squared Error (MSE), R-squared (R²), Mean Absolute Error (MAE), and Root Mean Squared Error (RMSE). Among the three models, LightGBM achieved the highest accuracy with the lowest MSE and the highest R², making it the most effective in minimizing prediction errors.
Despite the impressive performance of these models, certain limitations were noted, including the relatively high MAE of 0.0705, which indicates that while the models make good predictions, there is still room for improvement in precision, especially for specific data points. Additionally, the models’ reliance on geographical, environmental, and historical data may still miss more granular, domain-specific features that could further optimize yield predictions.
Future efforts should enhance the dataset by incorporating additional variables that could explain the variance in oil palm productivity, such as soil conditions or pest-related factors. Additionally, improving the feature engineering process and exploring more complex models, such as deep learning techniques, could further improve the predictive power and interpretability of the model. By refining these aspects, the models could provide even more actionable insights, aiding plantation managers in making informed decisions to optimize oil palm yield and productivity in the long term.


### Data set Link: 
https://springernature.figshare.com/articles/dataset/Additional_file_2_of_Limited_impacts_of_climatic_conditions_on_commercial_oil_palm_yields_in_Malaysian_plantations/21077345?file=37404752
