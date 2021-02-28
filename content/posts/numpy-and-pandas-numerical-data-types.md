---
title: Numpy and Pandas numerical data types
subtitle: 'Stability, Speed and Memory Usage.'
date: '2021-02-28'
thumb_img_alt: Man holding Pizza
content_img_alt: lorem-ipsum
excerpt: Do you know that 0.1 + 0.2 == 0.3 will gives False in programming language?
seo:
  title: ''
  description: ''
  robots: []
  extra: []
  type: stackbit_page_meta
layout: post
thumb_img_path: images/pexels-polina-tankilevitch-4109048 (1).jpg
content_img_path: images/pexels-polina-tankilevitch-4109048 (1).jpg
---
Original photo by [**Polina Tankilevitch**](https://www.pexels.com/@polina-tankilevitch?utm_content=attributionCopyText\&utm_medium=referral\&utm_source=pexels) from [**Pexels**](https://www.pexels.com/photo/food-woman-winter-fun-4109048/?utm_content=attributionCopyText\&utm_medium=referral\&utm_source=pexels)

What could go wrong if I use float32 instead of float64 ?\
I need more speed for my calculation without changing my code alot, is changing data types coud help me?\
I have limited RAM for processing huge dataset, what does this post means to me ?\
The goal of this post is to answer these question, focusing on speed and precision, without much tough about how it implemented. I’m assuming you to have some familiarity with Python, Numpy and Pandas.

> If number is a stick, and variable is a hole. Using a big hole to store a small stick is wasteful. What worse is putting a huge stick to a small hole.
> <cite>Vinson Ciawandy</cite>

## Numerical Stability

We need to make sure our number calculated correctly. Floating number (in almost every programming language that i know) have some unavoidable inaccuracies. This is the most famous example of such case.

![](https://ik.imagekit.io/pwhcix71iqy/0.1\_0.2\__0.3\_mZQjarmCOQLb.png)
<cite> Visit this website to understand this issue <https://0.30000000000000004.com/> </cite>

Most of the time, this kind of innacuracies are tolarable. But, there are some cases where this kind of behaviour is unacceptable. Here’s the example of such case :

![](https://ik.imagekit.io/pwhcix71iqy/image\_2020-11-17\_174514\_mGIYHMqcB.png)Calculating average from a huge pandas series can yield very different result if you use the wrong datatype. That’s why it is important to always do sanity checking to your data and code.  
For float16, the average is nan. Why? After some exploration, i notice that pandas series using np.mean for calculating average and [np.mean](https://github.com/numpy/numpy/blob/2582c681082e6c2c74d424e255afa8efefa4f899/numpy/core/\_methods.py) start with summing all the values and then dividing the sum by count of the values. Since float16 can store number only up to [65504,](https://stackoverflow.com/questions/3477283/what-is-the-maximum-float-in-python) storing number bigger than that will yield to Inf

```python
import numpy as np
np.array(100000.0,dtype=np.float16)
> array(inf, dtype=float16) # Output
```

I’m still not sure why calculating mean resulted in nan instead of Inf, but my point still not change that using the wrong data type could led you to wrong result.
