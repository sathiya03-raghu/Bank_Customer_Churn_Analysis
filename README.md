Bank Customer Churn Analysis

Project Overview

The Bank Customer Churn Analysis project aims to investigate customer behavior at a European bank, focusing on understanding the factors that contribute to customer churn. By analyzing account information and demographic data for 10,000 customers, we seek to identify key attributes associated with churn, build predictive models, and visualize trends in customer behavior.

Objectives

Identify Common Attributes of Churners: Analyze which customer features (e.g., age, balance, credit score) are more prevalent among customers who have churned compared to those who have not.

Predict Customer Churn: Develop a logistic regression model to predict the likelihood of a customer churning based on various demographic and account-related factors.

Explore Customer Demographics: Examine the overall demographics of the bank's customers, including age distribution, balance levels, and churn rates across different geographic segments.

Segment Customer Behavior: Investigate differences in account behavior among customers from Germany, France, and Spain to understand regional trends in churn.

Dataset

The dataset used for this analysis contains account information for 10,000 customers and includes the following attributes:

CustomerId: A unique identifier assigned to each customer. It helps distinguish one customer from another in the dataset.

Surname: The last name of the customer. This attribute can be used for identification but is generally not used in analysis due to privacy concerns.

CreditScore: A numerical value representing the customer's creditworthiness. Higher scores typically indicate better credit risk and may influence lending decisions.

Geography: The country or region where the customer resides (e.g., Germany, France, Spain). This attribute can help analyze geographic trends in customer behavior.

Gender: The gender of the customer (e.g., Male, Female). This attribute can be used to analyze demographic trends and preferences.

Age: The age of the customer. Age can be a significant factor in analyzing customer behavior and preferences.

Tenure: The number of years the customer has been with the bank. Longer tenure may indicate customer loyalty and can influence churn rates.

Balance: The current balance in the customer's bank account. This financial attribute can provide insights into the customer's financial health.

NumOfProducts: The number of bank products the customer is using (e.g., savings account, credit card, loan). This can indicate customer engagement and loyalty.

HasCrCard: A binary indicator of whether the customer has a credit card (1 = Yes, 0 = No). This can help analyze the relationship between credit card ownership and churn.

IsActiveMember: A binary indicator of whether the customer is currently an active member of the bank (1 = Yes, 0 = No). This attribute is crucial for assessing customer engagement.

EstimatedSalary: The estimated annual salary of the customer. This attribute can provide insights into customer segments based on income levels.

Exited: A binary indicator of whether the customer has churned (1 = Churned, 0 = Not churned). This is the target variable for churn prediction analysis. 


The raw dataset is available in the data/Bank_churn.csv file.

Methodology

The project follows these key steps:

Data Cleaning: The data was cleaned and preprocessed to handle missing values, remove duplicates, and convert categorical variables into appropriate formats for analysis.

Tools: Excel for Data Cleaning and R for Data Visualization

Exploratory Data Analysis (EDA): Conducted a thorough analysis to visualize key trends and relationships in the data. This included:

Summary statistics to understand the distribution of features.
Bar plots and box plots to compare churners and non-churners across various attributes.
Identification of outliers and patterns in customer behavior.

Model Development: Built a logistic regression model using the glm() function in R to predict customer churn. The model included the following predictors:

Age
Credit Score
Geography
Gender
Balance

Visualization: Created visualizations to communicate findings effectively. This included charts and plots to show churn rates by geography and customer demographics.

R Code for Bank Customer Churn Analysis

1. Load Required Libraries

# Load necessary libraries
library(readr)      # For reading CSV files
library(ggplot2)    # For data visualization
library(dplyr)      # For data manipulation

2. Read the Dataset

# Read the churn data CSV file
churn_data <- read_csv("C:\\Users\\ragur\\OneDrive\\Desktop\\Capstone Project\\Capstone\\Bank_churn.csv")

3. Data Cleaning and Preparation

# Check for missing values in the dataset
missing_values <- colSums(is.na(churn_data))

# Create Balance to Salary Ratio
churn_data <- churn_data %>%
  mutate(Balance_to_Salary_Ratio = Balance / EstimatedSalary)

# Convert 'Exited' to factor for modeling
churn_data$Exited <- as.factor(churn_data$Exited)

4. Summary Statistics and Basic Analysis

# Summary of churn data

summary(churn_data)

# Grouping data by HasCrCard and summarizing average age, balance, and credit score
HasCrCard_data <- churn_data %>%
  group_by(HasCrCard) %>%
  summarize(Avg_Age = mean(Age, na.rm = TRUE), 
            Avg_Balance = mean(Balance, na.rm = TRUE), 
            Avg_Credit_Score = mean(CreditScore, na.rm = TRUE))

5. Visualization of Churn by Geography

# Plotting churn by geography
ggplot(churn_data, aes(x = Exited, fill = Geography)) +
  geom_bar(position = "dodge") +
  labs(title = "Churn by Geography", x = "Churn Status", y = "Count")

6. Average Balance and Churn Rate by Geography

# Calculate average balance and churn rate by geography
geo_behavior <- churn_data %>%
  group_by(Geography) %>%
  summarize(
    Avg_Balance = mean(Balance, na.rm = TRUE), 
    Churn_Rate = mean(Exited == 1, na.rm = TRUE)
  )

7. Logistic Regression Model for Churn Prediction

# Building a logistic regression model to predict churn
churn_model <- glm(Exited ~ Age + CreditScore + Geography + Gender + Balance + HasCrCard + IsActiveMember, 
                   data = churn_data, family = "binomial")

# Displaying the summary of the model
summary(churn_model)

8. Additional Visualization

# Visualizing the relationship between HasCrCard and churn
ggplot(HasCrCard_data, aes(x = HasCrCard, fill = Exited)) +
  geom_bar(position = "dodge") +
  labs(title = "Churn by Credit Card Ownership", x = "Has Credit Card", y = "Count")


Model Evaluation: Evaluated the model's performance using metrics such as accuracy, precision, and the confusion matrix to assess how well it predicts customer churn.



Results

Churn Factors: Identified that customers with lower balances and credit scores were more likely to churn. The analysis showed significant churn rates among specific demographics and regions.

Predictive Model: The logistic regression model achieved an accuracy of XX% in predicting churn, demonstrating its potential for future applications in customer retention strategies.

Customer Segmentation: Notable differences in churn behavior were found among customers from different countries, highlighting the need for tailored marketing strategies.


Conclusion

This project provides valuable insights into customer behavior at the bank and offers predictive capabilities to inform decision-making around customer retention strategies. The findings can guide targeted interventions to reduce churn rates and improve customer satisfaction.
