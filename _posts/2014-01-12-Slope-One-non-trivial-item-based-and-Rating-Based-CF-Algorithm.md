---
layout: post
title: Slope One, non-trivial item-based and Rating-Based CF Algorithm 
description: ""
modified: 2014-01-12
tags: [Data Sets, Recommender Systems]
image:
  feature: codewp1.jpg
  credit: www.pointerplace.us
  creditlink: http://www.pointerplace.us/category/technology/
---


* References 
    *  wikipedia -> [Slope One](http://en.wikipedia.org/wiki/Slope_One)
    *  [Paper](http://lemire.me/fr/documents/publications/lemiremaclachlan_sdm05.pdf) -> From [Daniel Lemire](https://github.com/lemire?tab=repositories) & Anna Maclachlan
* Previous Solution
    *  using linear regression f(x) = ax+b, leading to severe overfitting
* Alternative Solution
    *  learn a simpler predictor (called slope one) , f(x) = x+b
* Examples 
    *  wikipedia provides good examples, please refer to ["Slope one collaborative filtering for rated resources"](http://en.wikipedia.org/wiki/Slope_One)  
* Features
    *  subtract the rating of the two items
    *  For each user, predict the <item, rating> pairs of those items this user has not rated.
    *  predict another user's rating of those items
    *  support both online queries and dynamic updates
    *  reduces storage requirements and latency
    *  scalable with respect to the number of users
    *  deprecated in Mahout 0.8
* Drawback
    *  Predicted ratings of some items sometimes are larger than 5. (Need to figure out what's wrong here.)
* Datasets 
    *  [MovieLens](http://grouplens.org/datasets/movielens/)  
* Source Code
    *  [Mahout taste API](http://grepcode.com/file/repo1.maven.org/maven2/org.apache.mahout/mahout-core/0.8/org/apache/mahout/cf/taste/impl/recommender/slopeone/SlopeOneRecommender.java#SlopeOneRecommender)  
* Practice
    *  [My sample code](https://github.com/faustineinsun/AIExamples/blob/master/Java/src/main/java/feiyu/com/collaborativefiltering/SlopeOneRecommenderExample.java)  

