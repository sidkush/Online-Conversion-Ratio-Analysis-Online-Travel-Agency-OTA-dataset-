# Online Hotel Booking Analysis

## 1. Business Problem Statement
An online hotel booking agency wants to analyze their dataset to understand user behavior and improve their conversion rates. The dataset contains information about users visiting the website, searching for hotels, and deciding whether to book a hotel or not. The main objective is to predict if a user will book a hotel based on various features and to identify the key factors influencing the booking decision.

## 2. Methodology
The analysis was conducted using the following methodology:

1. Data Cleaning:
   - Handled missing values in features like user_hist_stars, user_hist_paid, log_click_proportion, booking_value, and competitor data.
   - Treated outliers in price_usd and distance_to_dest using power transformation with box-cox transformations.
   - Combined features to reduce dimensionality, such as creating total_travellers by adding adults and kids, and is_converted indicating if a user clicked and booked.
   - Created price_usd_corr to represent the average mean price per room per night.

2. Exploratory Data Analysis (EDA):
   - Calculated click-through rate (CTR) and conversion rate (CVR) to understand user engagement.
   - Extracted weekday and month from the timestamp for further analysis.
   - Conducted a chi-square test between listing_review_score and listing_star, revealing that high star ratings (3-5) with review scores between 3.5-4.5 generate maximum conversions and click responses.
   - Filled missing values in distance_to_dest and location_score2 using Random Forest Regressor.

3. Model Selection:
   - Focused on predicting the 'booked' variable, which indicates if a user will book a hotel or not.
   - Handled the imbalanced dataset using techniques like SMOTE and balanced class weights.
   - Evaluated models based on the F1 score to minimize false positives and false negatives.
   - Compared the performance of Logistic Regression and Random Forest Classifier.

## 3. Key Findings from EDA
- Users are spending more money on major chain hotels.
- Users are not significantly influenced by hotel promotions, except for competitor1 hotel rates.
- Lowest sales were observed on New Year's Day 2013 and every Saturday.

![EDA Findings][]

## 4. Model Performance
The following models were evaluated for predicting the 'booked' variable:

| Model                                 | F1 Score | Accuracy | Precision |
|---------------------------------------|----------|----------|-----------|
| Logistic Regression (without SMOTE)   | 0.67     | 0.60     | 0.68      |
| Logistic Regression (balanced class)  | 0.90     | 0.86     | 0.85      |
| Random Forest Classifier (max_depth=8)| 0.89     | 0.85     | 0.85      |

Both Logistic Regression with balanced class weights and Random Forest Classifier performed well, with high F1 scores and accuracy. The balanced class approach helped in handling the imbalanced dataset effectively.

## 5. Solution and Approach
To predict if a user will book a hotel, the following approach was used:

1. Data Preprocessing:
   - Selected data where clicked=1, as a user can only book a hotel if they have clicked on the website.
   - Used this filtered data as the training set to predict the 'booked' variable for the remaining dataset.

2. Model Training:
   - Trained Logistic Regression with balanced class weights and Random Forest Classifier with a maximum depth of 8.
   - Evaluated the models using F1 score, accuracy, precision, and AUC-ROC.

3. Feature Importance:   - Identified the top 10 important features that influence the booking decision, including random sort, total_price, booking_window, length_of_stay, listing_position, price_usd_corr, log_historical_price, num_total, location_score2, and site_id.

For example, let's consider a user who has clicked on a hotel listing with the following features:
- total_price: $150
- booking_window: 7 days
- length_of_stay: 3 nights
- listing_position: 2
- price_usd_corr: $120
- log_historical_price: 4.8
- num_total: 2 travelers
- location_score2: 4.2
- site_id: 5

Based on these features, the trained model can predict the probability of the user booking the hotel. If the probability exceeds a certain threshold (e.g., 0.6 for Random Forest Classifier), the model will predict that the user will book the hotel.

## 6. Conclusion
The online hotel booking analysis revealed important insights into user behavior and factors influencing hotel bookings. By applying data preprocessing techniques, conducting exploratory data analysis, and training machine learning models, we were able to predict if a user will book a hotel with high accuracy.

The key findings suggest that users prefer major chain hotels, are not significantly influenced by promotions, and have lower booking rates during specific periods like New Year's Day and Saturdays. The top 10 important features identified can guide the firm in focusing their efforts to improve conversion rates.

Both Logistic Regression with balanced class weights and Random Forest Classifier performed well in predicting hotel bookings. The firm can choose either of these models based on their specific requirements and deploy them to make data-driven decisions and optimize their online booking platform.

By leveraging the insights gained from this analysis, the online hotel booking agency can enhance user experience, target marketing strategies, and ultimately increase their conversion rates.

