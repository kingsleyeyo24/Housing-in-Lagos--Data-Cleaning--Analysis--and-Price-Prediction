# Housing in Lagos: Data Cleaning, Analysis, and Price Prediction

### Project Overview

Lagos, Nigeria, is a rapidly growing city with a dynamic real estate market. However, housing prices vary significantly based on multiple factors, including location and property features. This project aims to clean, analyze, and build predictive models for house prices in Lagos to provide insights and data-driven pricing estimates.

### Data Source

The dataset for this analysis is sourced from OpenAfrica (https://openafrica.net/it/dataset/cost-of-housing-in-lagos)

### Tools

- Python (Jupyter Notebook)
- Tableau

### Imports

I imported key libraries to handle data processing, visualization, and machine learning for the Lagos housing analysis and price prediction.

- pandas – For data loading, cleaning, and manipulation.
- seaborn & matplotlib – To visualize trends, distributions, and correlations in the dataset.
- LinearRegression – The core model for predicting house prices.
- mean_absolute_error – To evaluate model performance by measuring prediction accuracy.
- train_test_split – For splitting data into training and testing sets, ensuring proper validation.
- check_is_fitted – To verify that the model has been trained before making predictions.
- 
![Image](https://github.com/user-attachments/assets/a35c04c8-730f-4573-acde-c392eddf179d)

### Data Wrangling

I designed this 'wrangle()' function to clean and preprocess the Lagos housing dataset for analysis and modeling.

- Price Cleaning: Removed /year and /day, stripped commas, and converted values to float for numerical consistency.
- Feature Extraction: Used regex to extract numeric values from Bedrooms, Bathrooms, and Toilets, filled missing values with 0, and converted to int.
- Outlier Removal: Filtered prices outside ₦100,000–₦40M to eliminate unrealistic listings.
- Encoding: One-hot encoded City and Neighborhood, dropping the first category to prevent multicollinearity.

![Image](https://github.com/user-attachments/assets/d9fa3b72-7337-41a3-8eee-733f2f459136)

### Exploratory Data Analysis (EDA)

- I used df.isnull().sum() to identify missing values in the dataset. 

![Image](https://github.com/user-attachments/assets/b91ff5df-6b82-4109-8174-ecb85a8d4600)

- I used df["Serviced"].unique(), df["Newly Built"].unique(), and df["Furnished"].unique() to inspect the distinct values in these columns. 

![Image](https://github.com/user-attachments/assets/bc26946e-4930-4413-83ac-9e48e6954d75)

- I used a boxplot to examine the distribution of house prices and detect outliers. I identified extreme outliers, with prices ranging from as low as ₦1 to as high as ₦1.7 trillion. I addressed this issue using the code in the **Data Wrangling** section.

![Image](https://github.com/user-attachments/assets/809d1cf3-165f-4ec0-b2ac-5278054a32cc)
