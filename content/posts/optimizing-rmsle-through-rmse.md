---
subtitle: for any machine learning and any programming language with a simple math trick
date: '2021-03-06'
seo:
  title: Optimize RMSLE through RMSE
  robots: []
  extra:
    - name: 'og:image'
      value: /images/optimize-rmsle-trough-rmse copy.jpg
      keyName: property
      relativeUrl: true
  type: stackbit_page_meta
  description: >-
    If you model can minimize RMSE, than your model can minimize RMSLE too with
    this simple trick.
layout: post
thumb_img_path: images/important-pineapple.jpg
title: Optimize RMSLE through RMSE
content_img_path: images/curious-rosemary.jpg
thumb_img_alt: Plane
content_img_alt: Plane
author: Vinson Ciawandy
excerpt: >-
  You need to optimize RMSLE(L for Logarithmic), but your model only know RMSE
  optimization.  Is there still anything love can do?
tags :
  - Math/Statistics
  - Optimization
---
<cite>Original photo by [Andrea Piacquadio](https://www.pexels.com/@olly?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/male-hand-with-white-toy-plane-3754680/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)</cite>

# What's the problem?

Sometimes, RMSE(Root Mean Squared Error) isn’t the best metric to solve your problem, so you decided to use RMSLE (Root Mean Square Logarithmic Error), or the competition you participate in are using RMSLE instead of the usual RMSE for judging criteria.

Some sophisticated libraries such as TensorFlow give the option to optimize RMSLE directly, but most of the machine learning libraries out there don’t support RMSLE optimization directly, but only for RMSE or MSE

in hurry for the trick? [jump here](#trick-for-optimizing-rmsle-trough-rmse)

# RMSE vs RMSLE
Let’s take a quick recap about the difference between these metric
{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image_2020-12-01_114510_GAR6szpSyqu.png" width="50%"> </img>
</div>
<br>

<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image_2020-12-01_114532__M_eAO9H24.png" width="75%"> </img>
</div>
{{</rawhtml >}}

By logarithmic property, RMSLE can be written as :
{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image_2020-12-01_114842_KBkOU2uI9z9p.png" width="55%"> </img>
</div>
{{</rawhtml >}}

By seeing this form, you should get that RMSLE focus on ratio between the actual value and the prediction value.  
Prediction = 10 with Actual = 100 gives roughly the same RMSLE with Prediction = 100 with Actual = 1000.  

Also, RMSLE are not symetric across the actual value. If we have actual value 500, prediction = 0 give higher RMSLE than prediction = 1000 (even tough both have distance 500 from actual value).

Because of these properties, intuitively minimizing RMSE ≠ minimizing RMSLE.

# Trick for optimizing RMSLE trough RMSE

If your machine learning libraries only support RMSE/MSE optimization while what you need is RMSLE optimization, then the trick is to transform your target variable so it share the same form as RMSLE.

{{<rawhtml>}}
<div align="center">
    <img src="
https://ik.imagekit.io/pwhcix71iqy/image_NGCmxZwbp.png" width="30%"> </img>
</div>
<div align="center">
<cite>log in here is natural logarithmic</cite>
</div>
{{</rawhtml >}}
    
You model the data using z as target instead of y. After getting the prediction, revert back the result with simple transformation 

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image_2020-12-01_135319_zXTuW4C9rcg.png" width="30%"> </img>
</div>
{{</rawhtml >}}

Here's the detail :
1. Do your EDA and feature engineering like usual
2. Transform the target variable into z = log(y+1)
3. Build machine learning model that optimized for RMSE/MSE to predict z
4. Transform your prediction result into y = exp(z) – 1

# Why this trick would works
I don’t have any rigorous proof about why this trick works, but I can give some intuitive explanation why this works.

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image_2020-12-01_190544_acSWo4M2U.png" width="55%"> </img>
</div>
<div align="center">
<cite>How do we optimize this? We should convert this into RMSE-lookalike form</cite>
</div>
<br>
{{</rawhtml >}}

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image-2_IIZ6lmflfFFm.png" width="30%"> </img>
</div>
<div align="center">
<cite>Let’s define our random variable z_i.</cite>
</div>
<br>
{{</rawhtml >}}

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image-3_zAeDC2RDIE.png" width="40%"> </img>
</div>
<div align="center">
<cite>Subtituting our new random variable</cite>
</div>
<br>
{{</rawhtml >}}

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image_2020-12-01_191711_BI4Y4b4yEqe.png" width="45%"> </img>
</div>
<div align="center">
<cite>Basically every prediction are function of the input.</cite>
</div>
<br>
{{</rawhtml >}}

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/image-4_muxaWCbir.png" width="30%"> </img>
</div>
<div align="center">
<cite>Subtituting the right part and now our RMSLE have the exact form of RMSE</cite>
</div>
{{</rawhtml >}}

# Experimentation

I will use Python and R to demonstrate the technique into 2 different dataset.

For the first one I will use R & Caret to model [Bike Sharing](https://www.kaggle.com/c/bike-sharing-demand) Data.
I use caret because it able to automatically do hyperparameter tuning for my xgboost model.

```r	
library(caret)
library(lubridate)
library(MLmetrics)
data = read.csv("train.csv")
 
#Simple feature engineering
data$datetime = ymd_hms(data$datetime)
data$hour = hour(data$datetime)
data$day = wday(data$datetime)
data$year = year(data$datetime)
 
#Split the data into train and test set
train = data[0:9000,]
test = data[9000:nrow(data),]
 
#Define what variables we would use as predictor and respone
prediction_formula = formula(count~season+workingday+weather+temp+humidity+windspeed+hour+day+year)
 
#WITHOUT RMSLE TRICK
#Use 5-folds cross validation during hyperparam optimization
fitControl <- trainControl(method = "cv",number = 5)
model.cv <- train(prediction_formula,
                  data = train,
                  method = "xgbTree",  #use xgboost
                  trControl = fitControl) 
prediction = predict(model.cv,test)
 
#Convert negative prediction into 0
prediction = ifelse(prediction<0,0,prediction)
RMSLE(prediction,test$count)
> 0.6929696
 
#WITH RMSLE TRICK
#Transform the target variable
train$count = log(train$count+1)
model.cv <- train(prediction_formula,
                  data = train,
                  method = "xgbTree",
                  trControl = fitControl) 
prediction = predict(model.cv,test)
#Revert the prediction to the original scale
prediction = exp(prediction)-1
prediction = ifelse(prediction<0,0,prediction)
RMSLE(prediction,test$count)
> 0.3510241
```

The RMSLE on the test data significantly improve from 0.69 into 0.35 after applying this technique.

For the second experiment, I use Python and [PyCaret]() on Insurance Medical Dataset
```python
#Without RMSLE trick
from pycaret.datasets import get_data
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_log_error as MSLE
import numpy as np
from pycaret.regression import *
 
data = get_data('insurance')
train,test = train_test_split(data,train_size=0.75,random_state=2233)
 
reg1 = setup(train, target = 'charges', session_id=123, log_experiment=True, experiment_name='insurance1')
best_model = compare_models(fold=5)
 
predict_new = predict_model(best_model, data=test)
np.sqrt(MSLE(predict_new.Label,test.charges))
>> 0.43920470684686724
```

```py
#With RMSLE trick
from pycaret.datasets import get_data
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_log_error as MSLE
import numpy as np
from pycaret.regression import *
 
data = get_data('insurance');
train,test = train_test_split(data,train_size=0.75,random_state=2233)
 
train.charges = np.log(train.charges+1)
reg2 = setup(train, target = 'charges', session_id=123, log_experiment=True, experiment_name='insurance2')
best_model = compare_models(fold=5)
 
predict_new = predict_model(best_model, data=test)
predict_new.Label = np.exp(predict_new.Label)-1
np.sqrt(MSLE(predict_new.Label,test.charges))
>> 0.4318665993748389
```

By using PyCaret, the RMSLE decrease from 0.43920 to 0.43186