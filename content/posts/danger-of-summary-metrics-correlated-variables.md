---
title: Danger of Summary Metrics - Correlated Variables
subtitle: How different data can fall into same value and blind our analysis
date: '2021-04-11'
thumb_img_alt: lorem-ipsum
content_img_alt: lorem-ipsum
seo:
  title: ''
  description: ''
  robots: []
  extra: []
  type: stackbit_page_meta
layout: post
thumb_img_path: https://ik.imagekit.io/pwhcix71iqy/summary-statistics-correlation/summary-statistics_emLzlXhm2yC.jpg
content_img_path: https://ik.imagekit.io/pwhcix71iqy/summary-statistics-correlation/summary-statistics_emLzlXhm2yC.jpg
excerpt: >-
  "X1 and X2 have a super high correlation, let's drop one of them for feature
  selection".  Are really sure about that?
---
This post is a series of Statistical Fallacies series. Read other’s post about statistical fallacies : 

# Background

For me, there are 2 types of Exploratory Data Analysis(EDA), visual EDA and numeric EDA.  
While visual EDA can generate a beautiful insight, it needs the analyst’s creativity to interpret what’s behind the picture, 
Numeric EDA  this thing can be automated since we usually know what we are looking for. One pitfall of being too dependent only on numeric EDA is failing to grasp the meaning behind the data. In this post, I will explain a Statistical Fallacies called Danger of Summary Metrics, with feature selection on correlated variables as the study case.
I will assume the reader already familiar with correlation and PCA.

# Feature Selection and Correlation

Feature selection can be crucial sometimes if we have too many unrelated features. 
One type of popular feature selection is dropping highly correlated features, which is pretty simple, fast, and model-agnostic. I see some people love to use this technique, especially when building an automatic machine learning pipeline.

For those who don’t know, here’s the gist of the techniques : 
Calculate all correlation between the predictors
If there are a pair of predictors that have |correlation| > threshold, drop one of them

Let's say X1 and X2 are variables with correlation = 0.95. That means whenever X1 increases, X2 will also increase, and whenever X2 decreases, X1 also decreases. Well, our X1 and X2 behave nearly identical to each other, maybe it is redundant to keep both of them in our data?
Well, most of the time it is true, but there are conditions where this approach failed miserably.

Here’s an example of the condition I’m talking about :

This is a scatter plot with 2 numerical variables as a predictor, and the target variable is encoded in colors. Both X1 and X2 have a pretty strong correlation, and it seems that a simple linear classifier will do a great job classifying class A or B. 

X1 and X2 above in fact have a correlation greater than 0.95. Now, If we drop one of X1 or X2 because of high correlation, now even the mightiest algorithm like CatBoost or any kind of boosting won’t help you. Why? the proof is left as an exercise to the reader ;)

# Principal component analysis(PCA) and explained variance

Okay, now you know that blindly trusting correlation value might hurt your data and yourself. So you decided to use another preprocessing step for your correlated variables, named Principal Component Analysis (PCA), and decide to take the top K variables with a cumulative sum of explained variance equal to a certain threshold, maybe 95%

Some people said that PCA-result with 95% explained variance = data is 95% similar to the original one. Well, this statement is not wrong, but you’ll miss the important insight for believing that statement.
Here’s the chart of previous data after PCA

The first component has explained the variance ratio
0.99713768 and the second component have 0.00286232. Also, each component are orthogonal(just my fancy way to say the features are uncorrelated)
It looks like another simple linear classifier will make make a great job to classify class A and B. Again if we drop the second component just because it has really tiny explainability, what would happen to the classification? 

# Conclusion
 So, yeah. We have tons of awesome tools to analyze the data, but using it blindly can hurt the analysis. Numeric EDA which bases on the summary value gives a fast way to interpret the data, but visualization tends to give a bigger picture than just some number. 
