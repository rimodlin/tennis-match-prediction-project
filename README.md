# Tennis Match Prediction Project

## Introduction

With a rich history and a vast global outreach, Tennis is arguably the most popular sport in the world. Beyond its contributions to individual health and community engagement, tennis has become a powerful force when it comes to building international connections. Major tournaments, containing players from most of the major countries, attract tens of millions of viewers worldwide, creating a shared experience that transcends cultural and geographic boundaries. In this dynamic world of aces and volleys, tennis stands as a sport that reaches much further than meets the eye, influencing individuals and societies alike.

Our analysis focuses on individual tennis matches as we look to determine how to predict match outcomes and match durations. Through our initial studies, we found that a tennis match can be influenced by a wide variety of variables. As we dove into the relationships between these variables in our exploratory data analysis, we aimed to focus on questions that sought to discover how important match-specific statistics influence a tennis match. Through deep analysis and heavy discussion, we felt that these two questions would be interesting and important to explore further.

**Q1: Which match statistics are most useful in predicting the outcome of tennis matches in the Association of Tennis Professionals (ATP)?**

**Q2: Which match statistics are most useful in predicting the duration of matches in the ATP?**

For our first question, we investigated how to predict the winner of tennis matches using match statistics from about 15,000 matches in the Association of Tennis Professionals (ATP). Being able to predict match outcomes can be very useful in sports betting. If you can accurately predict who will win a match, you can bet on the right athlete and win money! Statistical prediction may not always be 100 percent accurate, but it can give people a competitive edge when placing bets, by using real data and evidence, rather than randomly choosing who will win or choosing based on a personal hunch. Another benefit of predicting the winner of tennis matches is for tennis players & coaches themselves. Knowing which match statistics are most helpful in predicting a winner, can allow tennis players to focus their practice on particular areas, such as perfecting their serves to earn more aces during matches.

For our second question, we examined how to predict the match duration, in minutes, of each match in our dataset. Knowing match duration can be helpful to tennis players and coaches alike, as endurance is important when it comes to performing well throughout long matches. Predicting how long a match will last, can help tennis players adequately train and prepare to perform well on the big day. Another interesting use of predicting match duration could be to help schedule matches, especially those that air on television. Allotting enough air time for each match can ensure that viewers don’t miss a minute of entertainment. Lastly, predicting match duration can help predict how much money might be made from those attending matches in-person. Perhaps, the longer a match is, the more money will be spent by attendees on concessions and merchandise.

## Data

Our primary dataset is Jeff Sackmann’s comprehensive tennis ATP match dataset, which covers match data from 1920 to the present day. This dataset is free and publicly available on GitHub, which makes it an ideal resource for our analysis. The dataset is organized into yearly files with singular match data, providing an easy-to-navigate and clear structure. For our project, we decided to use the ATP match dataset from 2016 to 2019 and 2022. Due to the changing climate of the sport, we were interested in recent data. Furthermore, we left out 2020 and 2021 as further analysis of the data revealed an abundance of NA entries that we concluded to be a result of tournaments being canceled during the pandemic.

Since one of our focuses was always on the prediction of match results, we cleaned our dataset accordingly. The way certain variables were structured, in which the winner and loser were already denoted in the name of the variable, made it difficult for further analysis to be applied. The dataset also included many variables that we were not concerned with and were subsequently removed during cleaning, two examples were player country and player ID. The variables we kept were match statistics that we concluded, through analysis, would have the most influential impact on our questions.

The variables in our data are mostly match statistics for the two players that competed in each match. **player1_ace** and **player2_ace** display the number of aces each respective player earned during the match. **player1_df** and **player2_df** are the number of double faults, **player1_svpt** and **player2_svpt** are the number of serve points, **player1_1stIn** and **player2_1stIn** are the number of first serves made, **player1_1stWon** and **player2_1stWon** are the number of first-serve points won, **player1_2ndWon** and **player2_2ndWon** are the number of second-serve points won, **player1_SvGms** and **player2_SvGms** are the number of serve games, **player1_bpSaved** and **player2_bpSaved** are the number of break points saved, and **player1_bpFaced** and **player2_bpFaced** are the number of break points faced. **player1_won** is a binary variable that displays 1 when Player 1 won the match and 0 when Player 2 won the match. **minutes** displays the duration of each match in minutes.

To predict the match outcome with regression analysis for question 1, we needed to find a way to randomize the player number and mask the match result. We defined a custom function, shuffle_players, to anonymize the dataset by randomly assigning match statistics to two hypothetical players - Player 1 and Player 2 - in each match record. This approach ensured the blind analysis’ integrity by obfuscating the identities of the winners and losers. Applying this function to the dataset, we ensured that each match’s data was individually randomized along with a binary outcome variable indicating whether Player 1 won.

After data cleaning and transformation, we were left with 14,472 observations and 20 variables. The table below provides a glimpse of the first 5 rows of data.

|player1_ace|player1_df|player1_svpt|player1_1stIn|player1_1stWon|player1_2ndWon|player1_SvGms|player1_bpSaved|player1_bpFaced|player2_ace|player2_df|player2_svpt|player2_1stIn|player2_1stWon|player2_2ndWon|player2_SvGms|player2_bpSaved|player2_bpFaced|player1_won|minutes|
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|15|6|78|51|38|14|11|10|11|0|2|70|50|32|7|10|3|5|1|129|
|1|0|50|33|21|8|9|3|6|7|2|78|49|34|16|10|8|9|0|98|
|1|2|96|64|50|20|16|1|4|24|3|120|80|62|20|16|6|7|1|164|
|6|0|45|33|25|8|8|0|0|2|1|38|27|17|1|7|4|8|1|53|
|6|2|48|35|22|4|8|3|7|6|4|41|25|22|10|8|0|0|0|68|

The bar chart below provides a closer look at a singular match and compares Player 1’s and Player 2’s stats.

![alt text](https://github.com/rimodlin/tennis-match-prediction-project/blob/main/Final-Paper--Group-9_files/figure-html/unnamed-chunk-3-1.png)

## Results

### Question 1

In our analysis, we began by filtering out a dataset to include all relevant statistics for our study. We then fitted a Generalized Linear Model (GLM) using a logistical approach in three distinct ways: one incorporating up to third-degree interactions, another with only two-variable interactions, and a third with no interactions. Interestingly, all three models exhibited identical sensitivity, specificity, and other statistical measures. Consequently, we opted to use the simplest, no-interaction model. This choice was further validated when we conducted forward and backward selection processes on the no-interaction model, which indicated that all thirteen predictors were significant.

![alt text](https://github.com/rimodlin/tennis-match-prediction-project/blob/main/Final-Paper--Group-9_files/figure-docx/Correct, False Positive, and False Negative Scatter Plot - tennis prediction.png)

![alt text](https://github.com/rimodlin/tennis-match-prediction-project/blob/main/Final-Paper--Group-9_files/figure-docx/Correct, False Positive, and False Negative Bar Graph - tennis prediction.png)

Crucially, the final logistic model we selected through model selection and cross-validation processes demonstrated a remarkable accuracy of 94 percent, while the false positive rate and the false negative rate were merely 3 percent each. This high level of accuracy underscores the effectiveness of our model in predicting match outcomes based on the available data.

|Model|Sensitivity|Specificity|FPR|FNR|
|--|--|--|--|--|
|3 Way|0.9586207|0.916129|0.083871|0.0413793|
|2 Way|0.9586207|0.916129|0.083871|0.0413793|
|No Way|0.9586207|0.916129|0.083871|0.0413793|

Also, additional statistics to evaluate the accuracy of the model were calculated. The sensitivity of 0.94 indicates that our model had very few false negative results, and the specificity of nearly 0.93 verifies that our model was not susceptible to many false positive results. Furthermore, the very low false positive and false negative rates of 0.07 and 0.05, respectively, validate the accuracy of our model.

However, our study wasn’t without limitations. A key challenge was that the accuracy of the predictions, in terms of match results, relied on statistics available only after the completion of the matches. Despite this, our analysis still provided valuable insights into how various statistics in a tennis match could influence the outcome. These findings could be instrumental in future research, especially if we develop a system to store players’ past performances in the same tournament and use those statistics for predictive analysis.

Another limitation was the dataset’s scope. While it included a large number of matches, it lacked detailed elements crucial in tennis statistics, such as ball spins and speed. Access to more comprehensive match data could significantly enhance the quality of our models.

## Question 2

In our second question, we aimed to investigate the relationship between the duration of a match, measured in minutes, and various other match statistics. To conduct this, we excluded all Grand Slam matches because they are Best-out-of-five, while the rest of the tournaments are all best-out-of-3. For this particular question, we use the original dataset instead of the masked dataset we used for question one. To answer our research question, we initially developed a comprehensive model using match duration as the dependent variable, with other match statistics serving as predictors [**w_svpt**, **l_svpt**, **w_ace**, **l_ace**, **loser_rank_points**, **winner_rank_points**, **l_SvGms**, **l_df**, **w_1stWon**, **w_df**, **w_2ndWon**, **l_2ndWon**, **w_bpSaved**, **loser_rank**].

![alt text](https://github.com/rimodlin/tennis-match-prediction-project/blob/main/Final-Paper--Group-9_files/figure-docx/unnamed-chunk-12-1.png)

Despite achieving a promising mean absolute error (MAE) of 7.6, this model was potentially compromised by overfitting, a consequence of its large number of predictors.

To address this, we hypothesized that matches involving two players with closely matched statistics would tend to last longer. Based on this assumption, we refined our dataset, creating a new set of variables that quantified the absolute differences in player performance [**diff_1stIn**, **ace_diff**, **diff_2ndWon**, **bpSaved_diff**, **df_diff**, **SvGms_diff**, **diff_1stWon**, **svpt_diff**]. For example, **diff_1stIn** was calculated by: abs(**w_1stIn** - **l_1stIn**).

![alt text](https://github.com/rimodlin/tennis-match-prediction-project/blob/main/Final-Paper--Group-9_files/figure-docx/unnamed-chunk-13-1.png)

However, this simplified model, while simpler, exhibited a larger MAE of 25.2, indicating less accurate predictions. Both models presented unique challenges: the first model, while accurate, was complicated by a large number of predictors, increasing the risk of overfitting; the second model, in contrast, benefited from simplicity but at the cost of greater prediction errors. There are limitations to it as well. First, our model only serves as a way for us to understand the relationship between match duration and match statistics. Applying this model to real-life tennis matches would be difficult due to the same problem with the absence of full statistics before matches.

|Model|MAE|
|--|--|
|Model 1|7.553521|
|Model 2|25.191710|

The limitation of our first model would be the lack of applicability for the original intention of using the relationship between match statistics and match duration to strategize for the match. The first model relies on anticipating a specific number of aces, double faults, etc. for both players, which would be hard for players and coaches to do before the match. Therefore, the second model was developed using the differences in statistics because this is something that could potentially be predicted. For example, say you are a player who tends to double-fault a lot more than your opponent. The difference in double faults could potentially be estimated and used to run the model. The drawback to this is that the model employing the differences in statistics was significantly less accurate.

# Conclusion

Through our analysis, we answered two questions with our first question addressing which match statistics would best predict the outcome of tennis matches in the Association of Tennis Professionals (ATP), and our second question analyzing which match statistics are most useful in predicting the duration of matches in the ATP. To answer our first question we first had to create a new binary variable called **player1_won** with 1 representing Player 1 winning the match and 0 representing Player 2 winning the match. We then fitted a logistical model in three ways with different interactions where we found that all predictors had the same statistical results which led us to use a simple non-interactive model. With this non-interactive model, we did forward and backward selection and found that all thirteen of our predictors were significant. The final logistic regression we used had a high accuracy rate. For our second question, to find the most useful match statistics in predicting the match duration, we fit the model with minutes as a response and all other variables as predictors which gave us a high accuracy. We feel that this could be a result of potential overfitting due to the high number of predictors. Next, we looked to condense the data to show the difference in performance based on match statistics. The assumption is that players with similar statistics would have a longer match by modifying all of our existing variables to get the absolute difference between the players for each variable. We then found from this model that we had a greater error, despite it being simpler.

The results of our study in question 2 are significant as they offer a nuanced understanding of tennis match duration. By effectively predicting match duration based on comprehensive match statistics, our research provides valuable insights into the dynamics of tennis matches. The first model’s high accuracy, despite the risk of overfitting, suggests that detailed statistical analysis can be an effective tool in understanding and even anticipating match durations. This is particularly relevant for coaches and players, who could use such insights for strategic planning and training. Furthermore, our approach in the second model, focusing on the differences in player statistics, opens avenues for predictive analysis that could be more practical in real-time scenarios, such as during pre-match preparations.

The results from our analysis could be applied to many aspects of tennis, from game strategy to stadium revenue to sports bettings. The ability to predict the duration of a match can be used by stadium owners to forecast concession and merchandise purchases. Players and coaches can use this technology to condition players based on the anticipated grit of a match; if the match is expected to be long, players will be trained to conserve energy, and if the match is expected to be shorter, players will strategize to attack during the games while maximizing recovery during the breaks. Our proposed model that identifies key characteristics in determining match outcomes would be beneficial to sports bettors and sports betting agencies. Sports bettors can make better, well-informed decisions when placing their bets. It is also great for players and coaches to make match strategies based on the opponents.

In reflecting on our study, there are several areas where improvements could have been made to enhance the accuracy and applicability of our models. Although our models in question 2 aren’t ideal in predicting the match duration, we believe that other factors could play a role in determining this variable. Surface type could be important because certain surfaces are known to affect the speed of the ball. For example, grass courts have fast-moving balls, so players prefer to hit big serves and approach the net to finish the point quicker. On the contrary, clay courts have slower points, so players prefer to rally and sustain the point until their opponent runs out of stamina. Therefore, a model could potentially incorporate this variable to better predict match duration. A key area for improvement lies in the dataset itself. Our current dataset does not have information on some critical match statistics such as ball speed and spins, as well as placement of the ball on the court. Access to more detailed match statistics would have allowed for a more nuanced analysis. These factors play a crucial role in the dynamics of a tennis match and can significantly influence its duration and outcome. Additionally, exploring different statistical methods or more advanced modeling techniques could potentially yield better results. For instance, machine learning algorithms like Random Forest and SVMs might show complex patterns in the data that traditional models like GLM may miss.
