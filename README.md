# NFL-Win-Prediction-Project

## Introduction
This project aims to predict win percentages for all NFL Teams in the 2021 and 2022 seasons, based off of their performance in the past 5 years (2015-2020). 
Upwards of 73 million Americans place bets on the NFL each year, and there are more than 184m NFL fans. All of these fans place bets on their favorite teams either through sports betting platforms, or on family dinner tables. Thus, accurately predicting win percentages for all teams is a problem that 184m Americans face, and this is the problem I am trying to solve. 
## Datasets
Our data consists of eight years (2015-2022) worth of statistics from NFL statistics. Our training data is the first six years: 2015-2020, and our training data is 2021 and 2022. All of our data has been scraped from the pro-football-reference.com. 
## Experiments

### Linear Regression: 
I first performed a linear regression on all of the 22 variables I had available, and predicted the win percentages for each team in the 2021 and 2022 season. I obtained a R-squared value of 0.72, and a mean squared error 2.52. Two graphs were created, one showing the predicted win values in increasing order along with error bars representing the actual win totals for each team. The other shows the error between the model’s predictions and the actual win totals for each team in increasing order.

### Logistic Regression:
First, I added a new feature to the team data. The feature was a categorical variable that stated their postseason finish (i.e. No playoffs, Wild Card, etc). I then performed several logistic regressions using the same features I used on the linear regression in addition to the postseason feature. I created a regression to see if a team qualified in the postseason, then created regressions per each round of the postseason. The regression that predicted if a team qualified was accurate, but each subsequent round became harder to predict. I then took each team’s probabilities of winning the Super Bowl, ranked them, then took the six teams with the highest chances per 2021 and 2022.

### Regularized Regression:
First, I added a new feature to each of the samples which represented each team's strength of schedule for the given season (SOS). I then trained a Ridge Regression model on the updated data sets and validated the model using 5-fold cross validation. I tested multiple different 𝛼 values including [0.001, 0.01, 0.1, 1, 10, 100], and found that 𝛼 = 100 led to the best results with the MSE and R-squared being nearly identical to the OLS model. I then trained a Lasso Regression model to determine which features were necessary for making good predictions and to test the importance of the new SOS feature. Similar to the L2 regression model, I trained the L1 model using 5-fold cross validation and tested on the same alpha values, however for the L1 model the best 𝛼 was 0.01. The L1 model was able to achieve very similar MSE and R-squared values compared to the OLS and L2 model, however it only used 11 of the original 22 features. The newly added SOS feature was not included in the 11 non-zero weighted features which tells us that a team's strength of schedule is not helpful in estimating a team's predicted number of wins if I already have other stats such as yards per game, opponent yards per game, points for, and points against.


## Future Work
### Regular Season:
I could add more features, such as turnover differential, to see if this can improve the model. I can also expand the training data sample size by bootstrapping or by downloading more data from previous years. Additionally, I can try more regularization techniques to avoid overfitting.

### Playoffs:
Another way to implement postseason projections is to use a KNN model where each cluster is a postseason standing (e.g. division finish, wild card finish, did not qualify). Additionally, I could implement a decision boundary or SVM to categorize postseason team finishes. 

I could also use a regularization method to see which features for teams were the most important for their success, that way teams/fans can make better predictions on how far a team will go based on how well they’ve performed in a particular stat (e.g. fans whose team has a high PD can expect their team to have a good postseason run). I can also create decision trees that predict the entire postseason. The postseason can be represented in a hierarchical clustering or dendrogram. 

After the 2023 NFL regular season concludes, I can take this year’s data and use it in our models to predict this year’s postseason as well as see how many games the teams should have won. I can also take the data available so far this year and use it in the model that determines if a team is qualified to make it to the postseason. I can then predict which teams will make the playoffs this year using the results.


