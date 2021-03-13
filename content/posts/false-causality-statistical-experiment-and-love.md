---
title: False Causality - Statistical Experiment and Love
date: '2021-03-13'
seo:
  title: False Causality and Statistical Experiment
  description: ''
  robots: []
  extra: []
  type: stackbit_page_meta
layout: post
subtitle: >-
  I'm not an expert in love, but I hope my writing can give you an enlightment
  about love and most importantly, False Causality.
thumb_img_path: >-
  https://ik.imagekit.io/pwhcix71iqy/false_-_causality_-_Statistical_Fallacirs__1__-vtzzfm4x.png
content_img_path: >-
  https://ik.imagekit.io/pwhcix71iqy/false_-_causality_-_Statistical_Fallacirs__1__-vtzzfm4x.png
thumb_img_alt: a
excerpt: >-
  People tends to forget about existence of a third variable when concluding
  causality between two events.
---
<cite>Original photo by [Daria Shevtsova](https://www.pexels.com/id-id/@daria?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/id-id/foto/wanita-dengan-kemeja-flanel-bergaris-biru-memegang-buku-di-dalam-ruangan-698928/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) </cite>

# Brief intro to Statistical Fallacies  

So, what are Statistical Fallacies?
> "Misuse of Statistics: Using numbers in such a manner that – either by intent or through ignorance or carelessness – the conclusions are unjustified or incorrect.  
<cite>Spirer, Spirer & Jaffe 1998, p. 1.</cite>

So data can be easily manipulated or misunderstood to tell a different story from the truth. This post will tackle one of the most common forms of Statistical Fallacies, with the name **False Causality**

# Background
As an avid manga(Japanese comics) reader, I stumble in 1 book that introduces me to the world of statistical experimentation. No, I'm not talking about Manga Guide to Statistics, I'm talking about "Science Fell in Love, So I Tried to Prove It"

{{<rawhtml>}}
<div align="center">
    <img src="
https://ik.imagekit.io/pwhcix71iqy/Screen_Shot_2021-03-13_at_15.55.16_uihuKnSkf.png" width="70%"> </img>
</div>
<div align="center">
<cite>Here are our main characters who have feelings for each other </cite>
</div>
<br>
{{</rawhtml >}}

Hey hey hey, don't get me wrong. I'm not doing manga reviews on my blog, but I want to share what I learned from this manga.

# So What’s the story?
This is a story about two post-graduate researchers, Shinya and Himuro, who fell in love with each other. With their scientific-pride, they tried to gather evidences to prove their loves.
To make things easier to remember, I will call Shinya(the male MC) as **James** and Himuro(the female MC) as **Mary**

# The first experiment

The first way they try to prove their love is by measuring their heart rate. 
The hypothesis is “My heart rate will increase when I’m standing near someone I love”. Now I will create the **causal graph** from that statement. A **causal graph** is a graph where the vertex(the circle) represents an event and the edge(the arrow) represents which event will cause another event to happen. Let assume the causal graph like this :

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/causal-graph1_SdbS2lTnP.png" width="40%"> </img>
</div>
<br>
<div align="center">
<cite>This graph represents 2 events where the event of the left will causes(hyphotetically) the right event</cite>
</div>
<br>
{{</rawhtml >}}

For this experiment, they need a method to gather the **experimental data**.   
**Experimental data** is data where we assign people or things to groups and apply some treatment to one of the groups, while the other group does not receive the treatment. Observational data is data where we measure the sample without trying to affect them.  

Using **experimental data** is much preferable since we can minimize any unwanted distraction, but it needs a lot of energy and time to gather.

Here’s the experiment setup :
1. James will measure his heart rate alone as the **control group**
2. After that, James will measure his heart rate when he’s standing near Mary as the **experimental group**
3. From 2 heart rate measurement, do a t-test(or other statistical inference techniques) and search for evidence if his heart rate is higher when he’s standing near Mary

From the experiment, it turns out that James’ heart rate does increase when he stands near Mary. Does it mean his love proved? NO

It turns out that James’ heart rate will increase when he is standing near any beautiful woman. Even when there is a clear statistical significance of his heart rate, it doesn’t mean that Mary is the root cause of it.

# The 2nd experiment
Because of the first mistake, let’s rewrite the causal graph like this :

{{<rawhtml>}}
<div align="center">
    <img src="https://ik.imagekit.io/pwhcix71iqy/casual-graph2_x0jJ_hrFVzi.png" width="40%"> </img>
</div>
<br>
<div align="center">
<cite>We introduce new event in this graph</cite>
</div>
<br>
{{</rawhtml >}}

It turns out that the actual cause of the increasing heartbeat is to be together with a beautiful woman. That means, the previous study resulted in **False Causality**.
**False causality** is one of Statistical-fallacies, where a study concludes the wrong root cause of an event. One of the reasons this could happen is the existence of a **Confounding variable**.

**Confounding variable** is a variable that will affect two events together and cause false association between the two events.

In the manga, there are only 1 woman with James, so together with Mary = together with a beautiful woman.

Does that mean Mary is not the root cause of James increasing heart rate? We don’t know since we don’t have sufficient evidence to reject that hypothesis.

> “Rejecting hypothesis because there are no sufficient evidence is like taking a spoonful of water from an ocean and saying, there is no shark in the ocean because there is none in my spoon”
<cite>modified quotes from facebook</cite>

They need to design a better experiment, to get rid of the compounding effect. Here’s the setup :
1. James will measure his heart rate when he’s standing near a beautiful girl(not Mary) as the **control group**
2. After that, James will measure his heart rate when he’s standing near Mary as the **experimental group**
3. From 2 heart rate measurements, do t-test and search for evidence if his heart rate is higher when he’s standing near Mary
And the result? Read the manga if you want to know :p

# Summary
There are tons of **false causality** being deduced even among scientists. One way to avoid it is to design a **proper Experiment**, where the **control group** and **experimental group** differ ONLY by the treatment, not by other undetected factors like a **confounding variable**.
Running inferential statistics such as t-test on **observational data** would be improper to conclude a causality between events because there are many factors outside our scope.
