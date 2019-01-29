---
layout: post
title:      "Feature Selection "
date:       2019-01-29 01:01:11 +0000
permalink:  feature_selection
---

As we explore more basic concept of data science this is on of the most difficult section for newbie as well as exprience persion. The main reason for this is there might be more the 100's of independent data field in the data se you are dealing with.

Taking example of the 'King County House sales Dataset'
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sn
main_df = pd.read_csv("kc_house_data.csv")
data.shape

(21597, 21)
```

There total 21 data field in this dataset that means total 20 independent variables and 1 dependent variable.


Normally after performing the data cleaning i usually plot a Regresstion plot for each of the independent variable with respect to dependet variable and select those variable that are positively linear to the independent variabel.
```
sn.regplot(main_df.bathrooms,main_df.log_price)
```
![A regreation plot for Bathrooms and the price](https://imgur.com/mjLwB1C)

After going throught the plots i performs scaling and normalization on the data this help to get all the data in same range for later stages
# Removing MultiColinearrity
After the Data Scaling and normalization it is advised to check for the multicolinearrity in the independent variabels. most effecient way is by ploting the heat map from seaborn package.
![Heat Map](https://imgur.com/6ZGBJcN)
# Feature Slection using RFE
RFE stand for Feature ranking with **R**ecursive **F**eature **E**limination.
Scikit (sklearn) tool provide a very useful tool for the feature ranking. 
```
from sklearn.feature_selection import RFE
from sklearn.linear_model import LinearRegression
linreg = LinearRegression()
predictors = final_data.drop('log_price',axis=1)
selector = RFE(linreg, n_features_to_select = 2)
selector = selector.fit(predictors,final_data['log_price'])
```

Here the paramater  n_features_to_select is the pass by the analyst to see the different output of the model we can chnage this parameter.


