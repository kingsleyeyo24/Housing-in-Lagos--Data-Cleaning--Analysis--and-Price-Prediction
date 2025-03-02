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

- Used df["Price"].describe() to generate key summary statistics for house prices. I examined the price distribution by identifying the minimum, maximum, and 99th percentile values to ensure outliers have been removed.
  
![Image](https://github.com/user-attachments/assets/0d5e3fd1-6906-4fab-9507-b244ee9988bd)

### Data Analysis

- I calculated the average house price at two levels to understand price variations across locations:
  By City: Used groupby('City') to compute the mean price for each city, providing a broad market overview.
  By Neighborhood: Applied groupby('Neighborhood') to capture finer price differences within cities.

![Image](https://github.com/user-attachments/assets/a6287b00-b828-4d26-b6ef-2e4a513c51b0)

- I examined the bedroom counts to determine the most common number of bedrooms.

![Image](https://github.com/user-attachments/assets/5891fc8d-e02d-4df2-aacb-c9601a3e75ab)

I plotted the data using plt.bar() with a sky-blue color scheme for clarity. Labeled the axes and added a title to ensure the visualization is easy to interpret. Used plt.xticks(bedrooms) to make sure all unique bedroom counts are clearly displayed on the x-axis.

![Image](https://github.com/user-attachments/assets/231ff97a-3768-4b54-a4a5-55d1b5c29a7c)

- To compare house prices across cities based on bedroom count, I created a bar chart using Seaborn:
  I used sns.barplot() to plot average house prices per bedroom, grouped by city.
  I added labels and a title for clarity, ensuring the chart effectively communicates price trends.
  The legend highlights different cities, making it easy to compare price variations.
  
![Image](https://github.com/user-attachments/assets/f0bae759-1b46-4a55-8946-bbfdbe0030b2)

### Model Training & Evaluation

- To prepare the data for modeling, I split it into features (X) and the target variable (y):
  X – Contains all columns except "Price", "Title", and "More Info", keeping only relevant predictors.
  y – Stores the "Price" column, which serves as the target variable for prediction.
  
  ![Image](https://github.com/user-attachments/assets/f6027100-0986-4d9a-a713-565eafca3c8b)

- To train and evaluate the model effectively, I split the dataset into training (80%) and testing (20%) sets using train_test_split():
  X_train & y_train – Used to train the model.
  X_test & y_test – Reserved for testing to assess model performance.
  test_size=0.2 – Allocates 20% of the data for testing.
  random_state=42 – Ensures reproducibility of results.
  
![Image](https://github.com/user-attachments/assets/0b4364ad-2778-4a2f-9ee5-9511811d1089)

- I initialized and trained a Linear Regression model to predict house prices:
  model = LinearRegression() – Creates an instance of the linear regression model.
  model.fit(X_train, y_train) – Trains the model using the training dataset.
  
![Image](https://github.com/user-attachments/assets/18889623-ebaa-45bd-bb0f-a15748005caf)

- After training the Linear Regression model, I used it to make predictions on the test data:
  model.predict(X_test) – Generates predicted house prices based on the test set features.
  y_pred – Stores the predicted values for evaluation.
  
![Image](https://github.com/user-attachments/assets/d4f86809-fcb5-42f1-bdbf-27dc2acff06e)

- To measure how well the model predicts house prices, I calculated the Mean Absolute Error (MAE):
  mean_absolute_error(y_test, y_pred) – Computes the average absolute difference between actual and predicted prices.
  mae – Represents the model's error in Naira (₦), indicating how far predictions deviate from real values.
  Formatted Output – Displays the MAE rounded to two decimal places for clarity.

- To evaluate the model's performance, I calculated a baseline Mean Absolute Error (MAE) using a naive prediction:
  
![Image](https://github.com/user-attachments/assets/5e96e931-8ea8-43a6-9536-582aa79d6281)
A lower MAE means better model performance.

- To compare actual and predicted prices, I created a DataFrame that stores both values:
  "Actual" – Contains the real house prices from y_test.
  "Predicted" – Stores the model’s predicted prices from y_pred.
  
![Image](https://github.com/user-attachments/assets/29d6bc5f-fd27-4eea-bd69-a140f8b0ce4f)

- I re-initialized and retrained the Linear Regression model to refine its predictions:
  model = LinearRegression() – Creates a fresh instance of the model.
  model.fit(X_train, y_train) – Trains it again using the dataset.
  
  ![Image](https://github.com/user-attachments/assets/795ea0bc-dd8e-4da6-9fdd-2d10a67c9aea)
  This iteration allows for testing different preprocessing techniques, feature selections, or optimizations to improve performance.

– Checked if the model has been fitted to data.

![Image](https://github.com/user-attachments/assets/cfacd6be-c85f-421f-9fb6-736d4ea28906)

- To ensure the model's predictions align with the test dataset, I checked their lengths:
  model.predict(X_test) – Generates predicted house prices.
  print(len(y_pred), len(y_test)) – Compares the number of predictions to the actual test values.
  
![Image](https://github.com/user-attachments/assets/a20db6d1-7fb5-448b-96d0-812c537c2428)

- To assess how well the model predicts house prices, I plotted a scatter plot comparing actual and predicted values:
  sns.scatterplot(x=y_test, y=y_pred, alpha=0.5) – Displays predicted prices against actual values, with transparency for better visibility.
  plt.plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], 'r--') – Adds a diagonal reference line where perfect predictions would lie.
  Labeled Axes & Title – Ensures clarity in interpretation.
  
  ![Image](https://github.com/user-attachments/assets/527a753d-b627-4ade-a09e-0cae3ebd8fb0)

- To store the processed dataset for future use, I exported it as a CSV file
  
![Image](https://github.com/user-attachments/assets/69c81204-5be0-487f-965e-a262740d7c18)



