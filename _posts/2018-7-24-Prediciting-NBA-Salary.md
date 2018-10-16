---
layout: post
title: Predicting NBA Salaries
author: "Douglas Lee"
categories: journal
tags: [project, pandas, regression, nba]
image: NowitzkiWizards1.jpg
visible: 1
---

## Overview of Luther Project  

For my Luther project at Metis, I tried to predict NBA player salaries based using a linear regression model.   

Thanks to basketball-reference.com, most of the data I need were already fairly nicely formatted in static html pages. Using only BeautifulSoup, I was able to parse the player records I wanted and organize them into a pandas dataframe. After some cleaning to remove duplicate rows, rookies, and missing data, I fit a linear regression model based on only one feature, previous season average points per game (P_PTS), which had the second highest correlation with the target, current season salary(C_Salary). The highest correlation was previous season salary(P_Salary). I decided not to use P_Salary because I wanted to narrow my scope to predicting on a merit based model. In retrospect, this wasn't a great idea and really limited my model but I will come back to this later.  
  
My single variable linear regression model using P_PTS had a respectable R^2 score of 0.47, which suggests that about 47% of the variation in player salaries can be explained by their average points per game alone. To improve the model, I added three more features: previous season rebounds per game, previous season assists per game, and current age. I skipped many features that were next on the list in terms of correlation to the target, such as field goals per game, because they were also closely related to points per game. The four variable model had a R^2 score of 0.51, which waS a slight boost.   
  
The next step was feature engineering, such as taking polynomials of various features. I won't go into detail but the main idea is that while they did boost the R^2 score slightly, they were adding a lot of complexity to the model, thus decreasing interpretability. I also tested techniques such as standardizing the features and transforming the target to a log scale. Unfortunately, both of these techniques failed to improve the model within my setup. I was particularly disappointed in the logarithmic transformation of the target because the distribution did look a bit more symmetrical, if still skewed, after the transformation.   
  
In the end, I decided to pick the four variable model for the simple interpretaton despite its relatively poor performance. I also concluded that salary prediction likely requires a non-linear model because there was still a strong trend in the residual plot of the model despite my attempts to add more complexity.  
    
## Future Directions  
  
While I did make the conclusion that this might not be a linear regression problem, my analysis is not complete and there are many steps I can still take. 

1. First, I need to actually answer my question, which was predicting salary for a player getting a new contract. This was why I was worried about the P_Salary adding unwarranted confidence when their new contract should be based more on their stats than what they earned on their last contract. It may help to look at the subset of contract year players specifically to address this problem.  

2. The distribution of the salary is definitely not symmetrical. A non-linear model could help but it may also be worth modeling the salaries piecewise. Rookie salaries should be predicted based solely on their draft position because that is the ground truth, at least for those in the first round. It doesn't matter how well they end up doing; they are paid according to their position. On the other spectrum, there are the star players who may be worth more because of various things they bring that are not captured simply by stats, so I need additional features to captuer this relationship. A possibility is scraping their accolades information such as all star selections. Then there are the lower salary players who this model would really be relevant for. The NBA has a salary cap so max players will get their share but the mid tier players are the ones who can really influence how big of a contract they can get by their performance. 

3. Due to the two points above, I will expand my data set by scraping more seasons of data from each player. I restricted myself to only the past three seasons due to concerns over a sudden jump in the NBA salary cap but it left me with too few samples, only about 1000, to be split for all the subsetting I wanted to do. The sudden jump in the salary cap did result in some inflated contracts but it was a relatively minor group of players that a larger set of data can help mask. Adding the current year should help alleviate the impact of the gradual increase in salary over the years.  

4. Try cross interactions between features to see if I can capture more of that non-linear relationship. 