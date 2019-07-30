---
layout: post
title:      "Bank Loan Status Dataset"
date:       2019-07-30 12:04:23 -0400
permalink:  bank_loan_status_dataset
---


Finally, to module 3 that gave a detailed explanation of the classification process (Supervised and Unsupervised), this blog post will cover the explanation of the problem and my approach for the solution.

The biggest challenge for this project was to select the dataset. I browsed through the different website in search of a dataset that I can find it interesting. And finally, I chose the one from Kaggle, which was the Bank Loan Status Dataset. This dataset has over 100000 records and 19 features that perfectly fit the dataset requirement for the project. I chose this dataset because of the number of features it had and the data was somewhat clean and simple to understand. This saved a lot of time in scrubbing phase.

After having a brief discussion with my instructor my dataset was provided, the next thing I was told to find the feature I would like to predict from the dataset which was the Status of the loan.

The next steps which I took were using the OSEMN framework and implement my project accordingly.
![Data fram head](https://raw.githubusercontent.com/mitpatel5/dsc-3-final-project-online-ds-pt-112618/master/Images/Head.JPG)

In the first phase i.e. Obtaining the Data (O) I used the panda library to import the dataset into dataframe. After running bus basic commands (head, info, describe) I noted a few issues about the data that needed to be fixed in the next phase.

In the second phase i.e. Scrubbing / Cleaning (S) The data ask dataset was clean in terms of data presentation there were some issues. First of all, I remove 2 features as they were just for identification purpose and that won't help in the in predicting the outcomes. And rest of the issues are listed below:

1. There where various features with null values.
2. Dealing with categorical values.

![Nul Value Table](https://raw.githubusercontent.com/mitpatel5/dsc-3-final-project-online-ds-pt-112618/58ad296b64e88d70c16d475edeb923e474ed7e68/Images/table.JPG)

For the first problem, I made a function that takes the dataframe and input argument and iterates through each feature and prints a table with each feature and total missing values and % of total values. This table helped me to identify if I want to remove that feature or to fill the NaN with a value.

After the function was executed I got the feature “Months since last delinquent” had missing values of more the 53% so I decided to remove that feature.

The next thing that I noticed that there were 514 missing values in feature “Years of Credit History” so I pulled all the records that had null values in that feature and found out that last 514 records where just null records so I dropped them. 
![Null Tabel](https://raw.githubusercontent.com/mitpatel5/dsc-3-final-project-online-ds-pt-112618/master/Images/Null%20vales.JPG)

The Feature “Credit Score” and “Annual Income” had around 20k missing values I used the mean method to fill the null values.

The last one was a categorical feature “Years in current job” to fill that I used the mode method.
![Years At current job](https://raw.githubusercontent.com/mitpatel5/dsc-3-final-project-online-ds-pt-112618/master/Images/Years%20in%20current%20job.png)

In the third phase i.e. Explore Data (E) we basically get to know the data, we can plot a histogram to summarize the data attributes, plot a pair wire histogram to plot attributes against each other and highlight relationships and outliners.
![pair plot](https://raw.githubusercontent.com/mitpatel5/dsc-3-final-project-online-ds-pt-112618/master/Images/paiplot.png)

Now to encode the categorical data will help the model to understand the data with categorical values. So, here I have used pandas get_dummies function to encode my categorical data. Another important step was to remove the collinear features from the dataset with respect to the output feature.

Then we split the training set and test sets for both the input feature and the output feature with a test size of 0.2. 

`# Separate out the features and targets
features = credit.drop(columns='Loan Status')
targets = pd.DataFrame(credit['Loan Status'])

#Split into 80% training and 20% testing set
X_train, X_test, y_train, y_test = train_test_split(features, targets, test_size = 0.2, random_state = 42)

print(X_train.shape)
print(X_test.shape)
print(y_train.shape)
print(y_test.shape) `

As a part of feature scaling, I use Standard scaler to get more uniform distrubution for input features and apply label encoder on output features.
`from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test = sc.transform(X_test) `

`# Encoding the Dependent Variable
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_y_train = LabelEncoder()
y_train = labelencoder_y_train.fit_transform(y_train)
labelencoder_y_test = LabelEncoder()
y_test = labelencoder_y_test.fit_transform(y_test)
`

In the fourth phase i.e. Modeling we would apply the training sets to 5 different classification algorithem and test their accuracies. To make it easier we will create a function that takes the input arguments as training sets and model and return mean of the accuracies of the model.
` # Function to calculate mean absolute error
def cross_val(X_train, y_train, model):
    # Applying k-Fold Cross Validation
    from sklearn.model_selection import cross_val_score
    accuracies = cross_val_score(estimator = model, X = X_train, y = y_train, cv = 5)
    return accuracies.mean()`
		
Using the above function as:

`from sklearn.linear_model import LogisticRegression
logr = LogisticRegression()
logr_cross = fit_and_evaluate(logr) `


Accuracies for each model can be seen in the graph below 
![Final Plot](https://raw.githubusercontent.com/mitpatel5/dsc-3-final-project-online-ds-pt-112618/master/Images/plot.png)

1. Logistic Regression Performance on the test set: Cross Validation Score = 0.8197 (82%)
2. KNN Performance on the test set: Cross Validation Score = 0.7903 (79%)
3. Naive Bayes Performance on the test set: Cross Validation Score = 0.4193 (42%)
4. Random Forest Performance on the test set: Cross Validation Score = 0.8001 (80%)
5. Gradiente Boosting Classification Performance on the test set: Cross Validation Score = 0.8198 (82%)
