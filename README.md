# Dota2_match_predicter-analyse

Dota 2 is a multiplayer online battle arena (MOBA) video game developed and published by Valve. The game is a sequel to Defense of the Ancients (DotA), which was a community-created mod for Blizzard Entertainment's Warcraft III: Reign of Chaos. Dota 2 is played in matches between two teams of five players, with each team occupying and defending their own separate base on the map. Each of the ten players independently controls a powerful character, known as a "hero". There are currently 122 possible heroes to choose from, each with unique abilities and differing styles of play. During a match players collect experience points and items for their heroes to successfully defeat the opposing team's heroes in player versus player combat. A team wins by being the first to destroy the other team's "Ancient", a large structure located within their base.

![jpg](d2.jpg)

There are many different aspects of a match that contribute to the outcome of either a win or a loss. This analysis focuses on using various machine learning algorithms to create a model based on data collected within all information during the match of a high-ranking Dota2 match which as accurately as possible predicts the outcome of the match. Based on the resulting models, we will identify what elements of the game have the highest impact on the outcome of a match.

# Data Understanding
The data we will use to perform this analysis was obtained from this Kaggle dataset .This dataset contains 50000 ranked ladder matches from the Dota 2 data dump created by Opendota. 
The aim of this dataset is to enable the exploration of player behavior, skill estimation, or anything you find interesting. The intent is to create an accessible, and easy to use resource, which can be expanded and modified if needed. As such I am open to a wide variety of suggestions as to what additions or changes to make.

# Data preparation

First of all ,in our "match.csv" we can see all  information concerning the match (duration,fb,who won) ,but we could have not found any information about what happened in the match exactly.I mean there is no information about how much gold the radiant or dire team spent how much damage they did or we don't know their heroes.
So, the first step that I should do is group information by match  in (players.csv) where I can find more detail about the team's data and add this information to our base data.(['gold_spent','gold_per_min','xp_per_min','kills','deaths','tower_damage','hero_damage'] by each player)
The first 10 lines in this csv are representing our details ,but the problem is that in the nomral dota 2 matches there are two teams with 5 players within.
So we are grouping that information by 5 rows,and obtaining the mean value of each team in columns 
The first 10 lines in this csv are representing our details ,but the problem is that in the nomral dota 2 matches there are two teams with 5 players within.
So we are grouping that information by 5 rows,and obtaining the mean value of each team in columns['gold_spent','gold_per_min','xp_per_min','kills','deaths','tower_damage','hero_damage']).
There is a lot of columns in my opinion let's check the correlation for each column with the result  of the match which is radiant_win.


![jpg](correlation.jpg)

Then ,we drop useless columns like ['start_time','duration','game_mode','positive_votes','negative_votes','cluster'] because this columns dont influence on game result.


 
# Chosing the model
Before choosing the right model ,we should check the important features of data like (xp_radiant,gold_radiant)
Let's see the scatter plot with  linear regression.
![jpg](scatter.jpg)
Now that we have seen that there is some relationship between the total experience and gold and a team's win, we want to dive deeper into creating a model that puts together our features to as accurately as possible predict the outcome of a match and to identify which features have the highest impact on the match outcome.
Logistic Regression will be the least computationally costly model.

# Result of model

Let's plot the confusion matrix of our result and AOC to see the performance of our model.
![jpg](resultd2.jpg)

# Conclusion

Our model is showing us a good performance.Well,it's not a big deal because wins the team who has more xp and golds at the end of the match.
