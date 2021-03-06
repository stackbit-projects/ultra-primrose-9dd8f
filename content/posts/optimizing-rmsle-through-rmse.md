---
subtitle: for any machine learning and any programming language with a simple math trick
date: '2021-03-06'
seo:
  title: ''
  description: ''
  robots: []
  extra: []
  type: stackbit_page_meta
layout: post
thumb_img_path: images/optimize-rmsle-trough-rmse.jpg
title: Optimize RMSLE through RMSE
content_img_path: images/remarkable-whale.jpg
thumb_img_alt: Plane
content_img_alt: Plane
excerpt: >-
  You need to optimize RMSLE(L for Logarithmic), but your model only know RMSE
  optimization.  Is there still anything love can do?
---
<cite>Photo by [Andrea Piacquadio](https://www.pexels.com/@olly?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/male-hand-with-white-toy-plane-3754680/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)</cite>

# What's the problem?

Sometimes, RMSE(Root Mean Squared Error) isn’t the best metric to solve your problem, so you decided to use RMSLE (Root Mean Square Logarithmic Error), or the competition you participate in are using RMSLE instead of the usual RMSE for judging criteria.

Some sophisticated libraries such as TensorFlow give the option to optimize RMSLE directly, but most of the machine learning libraries out there don’t support RMSLE optimization directly, but only for RMSE or MSE

# RMSE vs RMSLE
Let’s take a quick recap about the difference between these metric
{{<rawhtml>}}
<div align="center">
<img src="https://ik.imagekit.io/pwhcix71iqy/conclusion_2021-02-20_UFaJlnFZz.png" width="100%"> </img>
</div>
{{</rawhtml >}}