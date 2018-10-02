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
The goal of this competition was to predict which "hotel group" (see [here](https://www.kaggle.com/c/expedia-hotel-recommendations/data) for more information) the customer will "book" on Expedia Website given an user event and its associated attributes. The dataset provided by Expedia contained two sets: The first set span from 2013 to 2014 and the second one included only 2015. The competitors were asked to predict top 5 hotel groups for each user event. More details of this competition can be found [here](https://www.kaggle.com/c/expedia-hotel-recommendations)


## Lessons I learned
Actually, this was my first time to apply machine learning models to real word problems after auditing the famous machine learning courses [Learning From Data](http://www.work.caltech.edu/telecourse.html) taught by [Prof. Abu-Mostafa](http://www.work.caltech.edu/) and its Chinese version [Machine Learning Foundation](https://www.csie.ntu.edu.tw/~htlin/mooc/) and [Machine Learning Techniques](https://www.csie.ntu.edu.tw/~htlin/mooc/) taught by [Prof. Lin](https://www.csie.ntu.edu.tw/~htlin/). It was an exciting experience to bring knowledge from book to practical problem and learn from the kaggle community :). Following are several takeaways of this competition:

### Before running any machine learning algorithm, make sure your data is trouble-free.

Although this practice might have been mentioned in many tutorials, workshops or courses. However, I still found it was non-trivial to make sure your data was trouble-free and it was the case in this competition. Some experienced kaggler reported that around one third of data suffer from the "data leak" (See this [link](https://www.kaggle.com/c/expedia-hotel-recommendations/discussion/20730) for the explanation under the scenario of this competition)

In the beginning, I did not notice the effect caused by leakage and applied XGBoost and random forest directly. It was until I found there was big gap between OOB error and the testing error did I realized the leakage might cause a serious problem (See [here](https://www.kaggle.com/c/expedia-hotel-recommendations/discussion/20831) for more discusion). To put it simply, the reason why my original method did not work well was that it completely memorized two features reported as leakage. Therefore, my model only relied on these two features to make "precise prediction". Sounds good, right? you got a correct prediction from these two features (user location, orig distance). 

The problem was there were only one-third of data had such features. For the others, my model completely lost the generality. Someone might wonder if this was the case, was it possible to impute the orig distance. My answer is yes and I recommend to check the [champion's solution](https://www.kaggle.com/c/expedia-hotel-recommendations/discussion/21607) (Although it was somehow brute force, I was still amazed by the creativity of the author to come out this solution), which outperformed the second place by 8%! I also tried other methods such as remove leaky features or split data into the leaky and the non-leaky part and leverage the leaky feature for the previous and trained a model on the non-leaky part. However, none of the above worked better than my final submission.

### Naive methods sometimes work well, not fancy,thoguh
My final submission was based on a very simple method: Recommendation of the most popular hotel group. The philosophy behind this method was: Let $U = \\{u_1, u_2,...,u_k \\}$ and $H = \\{h_1, h_2,...,h_p\\}$. A condition $c$ is defined as any subset of $U$ union with any subset of $H$. Given this condition, we count the most popular five hotel groups. That's it! with a penalty associated with time and a boolean feature click or book to the final counting number.

### Factrization Machine
It was until the end of the competition did I know what I was trying had had a more general and powerful method called [Factorization Machine](https://www.csie.ntu.edu.tw/~b97053/paper/Rendle2010FM.pdf). However, the interesting thing was that apply this method directly could not get a good result. I feel like it might be caused by leakage. This [tutorial](https://getstream.io/blog/factorization-machines-recommendation-systems/) give a clear example and code to play around:)

## Conclusion
This was my first competition and I was happy to get a decent rank. Although the whole competition involved many unexplainable hacks, it was still a great experience to compete with other Kaggler. One funny story I would like to share is: Because the first place won the other competitors by a large margin, many competitors had a hard time in the last week of competition. Enjoy this [thread](https://www.kaggle.com/c/expedia-hotel-recommendations/discussion/21458)!

