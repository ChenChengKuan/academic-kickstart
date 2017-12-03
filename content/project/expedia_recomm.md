+++
# Date this page was created.
date = "2016-06-11"

# Project title.
title = "Expedia Hotel \n Rec."

# Project summary to display on homepage.
summary = "Predict which hotel the customer will book (top 7%,121/1974)"

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "Expedia-logo.png"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["kaggle"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = true

# Optional featured image (relative to `static/img/` folder).
[header]
image = "headers/expedia_hotel_wide.jpg"
caption = "CCO:Common Creative"

+++

## Introduction
The goal of this competitoin is to predict which "hotel group" (see [here](https://www.kaggle.com/c/expedia-hotel-recommendations/data) for more information) the customer will "book" on Expedia Website given an user event and its associated attributes. The dataset provided by Expedia contained two set: The first set span from 2013 to 2014 and the second one contained only 2015. The competitors were asked to predict top 5 hotel groups for each user event. More details of this competition can be found [here](https://www.kaggle.com/c/expedia-hotel-recommendations)


## Lessons I learned
Acutally, this was my first time to apply some machine learnig models to real word problems after auditing the famous machine learning courses [Learning From Data](http://www.work.caltech.edu/telecourse.html) taught by [Prof. Abu-Mostafa](http://www.work.caltech.edu/) and its Chinese version [Machine Learning Foundation](https://www.csie.ntu.edu.tw/~htlin/mooc/) and [Machine Learning Techniques](https://www.csie.ntu.edu.tw/~htlin/mooc/) taught by [Prof. Lin](https://www.csie.ntu.edu.tw/~htlin/). It was an interesting experiences to bring knowledge from book to practical problem and learn from the kaggle community :). Following are several take-aways of this competition:

### Before running any machine learning algorithm, make sure your data is trouble-free.

Although this practice might have been mentioned in many tutorials, workshops or courses. However, I still found it was non-trivial to make sure your data was completely trouble-free and this happened in this competition. In this competition, some experienced kaggler reported that aronund one third of data suffer from the "data leak" (See this [link](https://www.kaggle.com/c/expedia-hotel-recommendations/discussion/20730) for explanation under the scenario of this competition)

At the begining, I did not notice the effect caused by leakeage and applied XGBoost and random forest directly. It was until I found there was big gap between OOB error and the testing error did I realized the leakage might cause serious problem (See [here](https://www.kaggle.com/c/expedia-hotel-recommendations/discussion/20831) for more discusion). To put it simply, the reason why my original method did not work well was because it completely memorized two features reported as leakeage. Therefore, my model only relied on these two features to make "precise prediction". Sounds good, right? you can get correct prediction from these two features (user location, orig distance). 

The problem was there were only one-third of data had such features. For the others, my model completely lost the generality. Someone might wonder if this was the case, was it possible to impute the orig distance. My answer is yes and I reommend to look the [champion's solution](https://www.kaggle.com/c/expedia-hotel-recommendations/discussion/21607)(Althought it was somehome brute force, I was still amazed by the creativity of the author to come out this solution), which outperformed the second place by 8%! I also tried other method such as remvoe leaky features or split data into leaky and non-leaky part and leverage the leaky feature for the previous and trained a model on non-leaky part. However, none of above worked better than my final submission.

### Naive methods sometimes work well and efficient, not fancy,thoguh
My final submission was based on a very simple method: Recommendation of the most popular hotel group. Let $U={u_{1},u_{2},...,u_{k}}$ and $H={h_{1},h_{2},...,h_{p}}$ were the attributes associated with users and hotels.
