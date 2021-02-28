---
title: Numpy and Pandas numerical data types
subtitle: 'Stability, Speed and Memory Usage.'
date: '2021-02-28'
thumb_img_alt: Man holding Pizza
content_img_alt: lorem-ipsum
excerpt: lorem-ipsum
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

What could go wrong if I use float32 instead of float64 ?  
I need more speed for my calculation without changing my code alot, is changing data types coud help me?  
I have limited RAM for processing huge dataset, what does this post means to me ?  
The goal of this post is to answer these question, focusing on speed and precision, without much tough about how it implemented. I’m assuming you to have some familiarity with Python, Numpy and Pandas.  

> If number is a stick, and variable is a hole. Using a big hole to store a small stick is wasteful. What worse is putting a huge stick to a small hole.
<cite>Vinson Ciawandy</cite>

Numerical Stability
We need to make sure our number calculated correctly. Floating number (in almost every programming language that i know) have some unavoidable inaccuracies. This is the most famous example of such case.