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

For the first problem, I made a function that takes the dataframe and input argument and iterates through each feature and prints a table with each feature and total missing values and % of total values. This table helped me to identify if I want to remove that feature or to fill the NaN with a value.

After the function was executed I got the feature “Months since last delinquent” had missing values of more the 53% so I decided to remove that feature.

The next thing that I noticed that there were 514 missing values in feature “Years of Credit History” so I pulled all the records that had null values in that feature and found out that last 514 records where just null records so I dropped them. 

The Feature “Credit Score” and “Annual Income” had around 20k missing values I used the mean method to fill the null values.

The last one was a categorical feature “Years in current job” to fill that I used the mode method.

In the third phase i.e. Explore Data (E) we basically get to know the data, we can plot a histogram to summarize the data attributes, plot a pair wire histogram to plot attributes against each other and highlight relationships and outliners.

Now to encode the categorical data will help the model to understand the data with categorical values. So, here I have used pandas get_dummies function to encode my categorical data. Another important step was to remove the collinear features from the dataset with respect to the output feature.

Then we split the training set and test sets for both the input feature and the output feature with a test size of 0.2. 

As a part of feature scaling, I use Standard scaler to get more uniform distrubution for input features and apply label encoder on output features.

In the fourth phase i.e. Modeling we would apply the training sets to 5 different classification algorithem and test their accuracies. To make it easier we will create a function that takes the input arguments as training sets and model and return mean of the accuracies of the model.

Accuracies for each model can be seen in the graph below 

