 # London House Price Prediction Using Machine Learning

An end-to-end machine learning project predicting residential property prices across London using property, geographic, transport and socio-economic data.

The project compares multiple regression models using a time-based validation strategy and investigates not only predictive performance, but also model errors and the factors influencing London property prices.

## Project Overview

Accurately predicting property prices in London is challenging because prices are influenced by property characteristics, location, accessibility and socio-economic conditions.

This project integrates multiple UK open datasets to build and evaluate machine learning models for London residential property price prediction.

Transactions from **2022-2023 were used for training**, while **2024 transactions were kept as an unseen test set**, providing a realistic temporal evaluation of how the models perform on future property transactions.

![Project Workflow](images/project_workflow.png)

## Data Sources

The project combines data from several publicly available UK sources:

- UK residential property transaction data
- ONS Postcode Directory (ONSPD)
- Index of Multiple Deprivation (IMD)
- Transport for London (TfL) station data

The final modelling dataset incorporates property characteristics alongside spatial and socio-economic information.

Key features include:

- Property type
- New-build status
- Tenure type
- Latitude and longitude
- IMD decile
- Distance to nearest transport station
- Distance to Central London
- Month of transaction

Raw and processed datasets are not stored in this repository due to their large file sizes. Further information is available in the [`data`](data/) directory.

## Methodology

The project followed an end-to-end machine learning workflow:

1. Data collection and integration
2. Data cleaning and preprocessing
3. Feature engineering
4. Temporal train-test split
5. Model development and hyperparameter tuning
6. Model evaluation
7. Error analysis
8. Permutation feature importance

Three regression algorithms were compared:

- ElasticNet
- Random Forest
- Histogram Gradient Boosting

Property prices were log-transformed during modelling to reduce the effect of the highly skewed London housing market.

## Model Performance

Random Forest produced the strongest overall performance on the unseen 2024 test data.

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| ElasticNet | £253,576.69 | £622,839.81 | 0.2099 |
| Random Forest | **£191,716.64** | **£502,547.67** | **0.4856** |
| HistGradientBoosting | £217,084.17 | £547,225.83 | 0.3901 |

The Random Forest model also achieved a **Median Absolute Error of £80,728.21**, with **33.09% of predictions falling within 10% of the actual sale price**.

## Predicted vs Actual Prices

The following plot compares Random Forest predictions with actual property prices on the unseen 2024 test set.

![Predicted vs Actual](images/predicted_vs_actual.png)

The model performs reasonably well across much of the housing market but tends to underestimate some high-value properties. This highlights the difficulty of predicting London's highly heterogeneous and expensive property market.

## Feature Importance

Permutation feature importance was used to investigate which variables contributed most strongly to Random Forest predictions.

![Feature Importance](images/feature_importance.png)

**Distance to Central London** was the most influential feature, followed by **tenure type**. Geographic coordinates, property type and deprivation level also contributed substantially to model performance.

This demonstrates the importance of combining conventional property characteristics with spatial and socio-economic information.

## Error Analysis

Model performance was investigated across different property types and price ranges rather than relying only on overall evaluation metrics.

### Error by Property Type

![Error by Property Type](images/error_by_property_type.png)

Prediction errors varied across property categories. Flats, terraced and semi-detached properties generally produced lower errors, while detached and other property types were more difficult to predict.

### Error by Price Band

![Error by Price Band](images/error_by_price_band.png)

Prediction errors increased substantially for higher-priced properties. The model performed more reliably for mainstream transactions, while luxury and unusual properties were considerably harder to estimate accurately.

## Tools and Technologies

The project was developed using:

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Jupyter Notebook / Google Colab
- Machine Learning Regression
- Feature Engineering
- Hyperparameter Tuning
- Permutation Feature Importance
- Spatial Data Analysis

## Repository Structure

```text
London-House-Price-Prediction/
│
├── data/
│   └── README.md
│
├── images/
│   ├── error_by_price_band.png
│   ├── error_by_property_type.png
│   ├── feature_importance.png
│   ├── predicted_vs_actual.png
│   └── project_workflow.png
│
├── notebooks/
│   └── london_house_price_prediction.ipynb
│
├── report/
│   └── London_House_Price_Prediction_Dissertation.pdf
│
└── README.md
```

## Project Files

- [`Jupyter Notebook`](notebooks/london_house_price_prediction.ipynb) - complete data preparation, feature engineering, modelling and evaluation workflow
- [`Dissertation Report`](report/London_House_Price_Prediction_Dissertation.pdf) - full academic report covering the methodology, results, discussion and conclusions
- [`Data Documentation`](data/README.md) - information about the datasets used in the project

## Key Findings

The analysis produced several important findings:

- Random Forest achieved the strongest overall predictive performance.
- Spatial and socio-economic feature engineering improved the modelling framework.
- Distance to Central London was the most influential feature in the final Random Forest model.
- Tenure type was the second most important predictor.
- Geographic location, property type and neighbourhood deprivation also contributed substantially.
- Prediction accuracy varied considerably across property types and price ranges.
- High-value and unusual properties were substantially more difficult to predict accurately.
- Hyperparameter tuning produced only modest improvements, suggesting that data preparation and feature engineering contributed more to model quality than extensive optimisation.

## Limitations

The project has several limitations:

- Detailed property-level characteristics such as floor area, number of bedrooms and property condition were unavailable.
- A geographic bounding box was used to define London rather than a formal administrative boundary.
- Only three regression algorithms were compared.
- Hyperparameter tuning was deliberately limited due to the size of the dataset and scope of the project.
- Performance was weaker for luxury and unusual properties.

## Future Work

Potential extensions include:

- Incorporating floor area, room count, EPC information and property condition
- Using more precise London administrative boundaries
- Adding richer neighbourhood and accessibility variables
- Comparing additional machine learning algorithms
- Exploring more advanced explainability methods such as SHAP
- Developing separate models for different property types or price segments

## Academic Context

This project was completed as part of my **MSc Data Science dissertation at the University of East London**.

The repository presents the work in a portfolio-friendly format and includes the original analysis notebook, selected visualisations and a cleaned copy of the dissertation report.

## Author

**Abdul Hadi**

MSc Data Science
