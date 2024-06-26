# Predicting Credit Card Fraud: 
## *A Comparison of Supervised Learning Models*
### UofT-DSI — Team Project 1 
### Group 2 — Sarita Rana, Elizabeth Yeo, Okky Rijanto, and Gordon Geringas


## Abstract
Global losses in credit card fraud have risen from over USD 18 B in 2014 to over USD 33 B in 2024 [(Statista)](https://www.statista.com/statistics/1394119/global-card-fraud-losses/). The timely detection of fraud and the application of interventions can help credit institutions attenuate impact of these crimes on a massive scale. There are many statistical models that could predict fraud from transaction data and each will yield a different accuracy. In order to aid in model selection we investigate the accuracy of several supervised learning models in predicting fraud.


## Introduction
Before forming our team we each filled out a survey of our research interests. Because of our shared interest in the Finance sector and machine learning techniques the four of us were selected to form Group 2. We searched for datasets that were highly rated for being well maintained and we filtered for financial focused data. We ultimately decided to use the [*"Credit Card Fraud"* dataset by Dhanush Narayanan R, accessed on Kaggle](https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud) for our [1st Team project](https://github.com/gordonmod8/team_project/blob/team-project-1/team_project_2.md). The data in this repository comes in a csv file and has a million rows. The dataset has 7 critical features for predicting fraudulent transactions and a boolean response for fraud listed:
1. distance_from_home
2. distance_from_last_transaction
3. ratio_to_median_purchase_price
4. repeat_retailer
5. used_chip
6. used_pin_number
7. online_order
8. fraud


Nearly universally folks have had personal experience with each of these predictors and credit card security incidents. Hence, these predictors were particularly compelling to study. We aim to use this data to quantify and compare the predictions of simple statistical learning models on all the available predictors. This kind of improvement in prediction precision will attenuate the financial impact of credit card fraud by locking more criminals out after the first suspicious transaction as well as reduce unnecessary service interruptions by lowering the rate of false positives. The credit institution will be able to better serve its customers and write off fewer losses.


## Rules of Engagement


The Group 2 team has four members: Sarita Rana, Elizabeth Yeo, Okky Rijanto, and Gordon Geringas. The analysis efforts were divided by statistical model and assigned to each team member. Initially each analysis was to be pushed to Github in a single notebook. But the tasks of diffing and merging the ipynb format was not a good match for Github's workflow. With a limited time budget for troubleshooting spent, the team resolved to split the analysis into multiple workbooks in the /src folder.


The scope of analysis techniques was reduced so as to apply just the techniques of our previous module in the Data Sciences Institute Certificate, "Applying Statistical Concepts". In the prior 3 weeks we studied Multivariable Regression, Logistic Regression, K-Nearest-Neighbours, Confusion Matrix and Correlation Matrix, Cross-Validation and Bootstrapping from the source [*"Introduction to Statistical Learning with Applications in Python"* by James, Witten, Hastie, Tibshirani and Taylor; published by Springer](https://www.statlearning.com/).


Our agendas at each meeting advanced the project's required deliverables. The first meeting initialized our repository and selected a data set of common interest. The second meeting divided the analysis by team members. The third meeting attempted merges and solved data analysis problems. The fourth meeting consolidated the findings and assigned the README efforts. The fifth meeting was editorial.


Agreement on team decisions was determined by a consensus of a quorum present in the Breakout Rooms on Zoom. A record of those team decisions and assigned deliverables was kept in Slack DMs. The low amount of formality was optimal since the team was a self-accountable unit. Project management solutions such as Jira or Trello were considered but ultimately rejected due to the lack of applicability of their features to the project's limited complexity, and duration.


## Models, Observations, and Challenges
1. **Exploratory Data Analysis (EDA)**  An initial analysis of the dataset was conducted to understand the cross-correlations and distributions of features and the extent of imbalance of the response. Summary statistics were calculated and with visualizations they helped suggest relationships between features and the target variable, fraud.
2. **Linear Regression**  We applied linear regression as a baseline model to understand the relationship between the features and the target variable. Although linear regression is not ideal for classification tasks, it provided a simple starting point for model development. We noticed all of the features have very low coefficient value, indicating they have very little influence on the target variable.
3. **Multiple Linear Regression with an interaction term**  The multiple regression results also had very low coefficients indicating the individual variables had very low correlation but when we modeled the regression for an interaction term between multiple variables, the coefficients were significantly higher suggesting that the variables together may have a higher accuracy in predicting fraud.
4. **K-Nearest Neighbors (KNN)**  The KNN model with K=3 was highly effective with a high accuracy of 99.8%. But High accuracy might be misleading if the dataset is heavily imbalanced. There is a risk of Minority Class Isolation resulting in a high accuracy. Fraudulent transactions, being rare, might not have enough neighboring instances of the same class. This can cause KNN to misclassify them as non-fraudulent because their nearest neighbors are mostly non-fraudulent transactions. In order to address imbalance, downsampling was investigated.
5. **Downsampling & Correlation Matrix Comparison**  Downsampling was employed to keep all of the positive fraud examples while randomly selecting variables from the rest of the data such that the resulting data frame was 50% fraud and 50% no fraud. The correlation matrix of the dataframe was compared with the initial exploratory data analysis. The coefficients of correlation showed significant gain across the board in the downsampled Data Frame. We predicted that training further learning models on downsampled data could improve the signal of fraud. We expected either improved precision, or we expected the rate of false positives to increase with the rate of false negatives decreased thus improving the attenuation of damages while incurring a lift in service interruptions.
6. **Notebook Merging Workflow Disruptions**  At this stage significant troubleshooting time was spent trying to merge our analysis work into one notebook. Although everyone wrote and resolved pull requests, the merges often corrupted the ipynb file and had to be pushed again which did not require merging since a corrupted file and legitimate file are not merged, simply the legitimate files overwrites the corrupted file. This double PR situation was resolved by accepting multiple ipynbs into the src folder which were pulled in from their respective branches.
7. **Logistic Regression**  The downsampled dataset was exported to a .csv and then loaded into a dataframe. The data was used to train a Logistic Regression learning model which was evaluated for precision and with a confusion matrix. The logistic regression was fairly good at predicting credit card fraud but had a bump in both false-negatives and false positives in comparison with KNN K=3 without downsampling.
8. **Random Forest**  The data was downsampled and a random forest model was trained. The performance of the model was evaluated against test data in the downsampled dataframe using [Area Under the Receiver Operating Characteristic](https://www.geeksforgeeks.org/auc-roc-curve/). This demonstrated an incredible bump in precision. In addition the confusion matrix displayed a significant reduction in both false positives and false negatives.


## Results and Conclusions


- Okky (Describe method to tabulate results seeking impact on credit institution value)
- Okky (find rates for table below)



| Model         | Precision | False Negative Rate | False Positive Rate |
|---------------|-----------|---------------------|---------------------|
| MVR           | 1.00      | 1.00                | 1.00                |
| KNN           | **1.00**  | 1.00                | 1.00                |
| LogR          | 1.00      | 1.00                | 1.00                |
| RndFor        | 1.00      | 1.00                | 1.00                |


- Okky (Results of comparison indicate (which model) has the best impact on (customer value) for the credit institution.)


## Videos of Learning and Experience (Links)


* Sarita Rana: https://drive.google.com/file/d/1J7-f0emnaJabHOkSX0Zo0YLDomFkHgPA/view?usp=drive_link
* Elizabeth Yeo: https://drive.google.com/file/d/16CQnj9jih-SSa84uT4QGoKti-7Boy8Pe/view?usp=drive_link
* Okky Rijanto:
* Gordon Geringas:


