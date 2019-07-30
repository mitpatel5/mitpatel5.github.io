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
![](https://github.com/mitpatel5/dsc-3-final-project-online-ds-pt-112618/blob/master/Images/Head.JPG)

In the first phase i.e. Obtaining the Data (O) I used the panda library to import the dataset into dataframe. After running bus basic commands (head, info, describe) I noted a few issues about the data that needed to be fixed in the next phase.

In the second phase i.e. Scrubbing / Cleaning (S) The data ask dataset was clean in terms of data presentation there were some issues. First of all, I remove 2 features as they were just for identification purpose and that won't help in the in predicting the outcomes. And rest of the issues are listed below:

There where various features with null values.
Dealing with categorical values.



