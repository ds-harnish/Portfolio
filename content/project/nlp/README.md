---
title: Sentiment Analysis of Reddit posts
summary: 'What are sentiments for Startrek and Starwars around the world? Used Reddit API to scrape data of ~12,000 posts to get the general sentiments in order to get marketing strategies right for upcoming series Star Trek: Discovery coming out in 2024.'

#tags:
#  - Demo
date: "2024-04-19T00:00:00Z"

# Optional external URL for project (replaces project detail page).
#external_link: https://github.com/dillondiatlo/Team2

image:
  caption: Photo by Toa Heftiba on Unsplash
  focal_point: Smart
---



# Project 3: Web APIs & NLP
--- 
## Introduction and Problem Statement
---
As part of the marketing team for the series Star Trek: Discovery coming out in 2024, the stakeholders have instructed our team to conduct a NLP research on Star Trek and our competitor, Star Wars using Reddit. As we will be working with various Search Engines to publish our advertisements, this research seeks to come out with a classification model for a more effective advertising campaigns for Star Trek. Besides the classification model, this research will also address the following:

- Identify some top common words to have a quick pilot test on the marketing campaign such as hashtags in instagram.
- Provide a general sentiment analysis on the community as compared to our competitor.

## Contents
---
- [Executive Summary](#Executive-Summary)
- [Data Collection](#Data-Collection)
- [Data Cleaning and EDA](#Data-Cleaning-and-EDA)
- [Preprocessing and Modeling](#Preprocessing-and-Modeling)
- [Conclusion and Recommendations](#Conclusion-and-Recommendations)

## Executive Summary
---
Star Trek television series was first released on September 8, 1966, and aired for three seasons, it then continued to air until 1974. After a hiatus, it came back stronger in 1988 and remained active for the next 17 years to 2005. It was only until recently (2018) that it had made another comeback to the television scene.

"Compassion: that’s the one thing no machine ever had. Maybe it’s the one thing that keeps men ahead of them." — Dr. McCoy

In the current era, the popularity of their competitor, Star Wars seems to be higher. To ensure Star Trek's continual relevancy in our modern world. A NLP research between the two would be important to gain some insights to carry out successful marketing campaigns in a more data-driven approach. To pioneer this research, we will look into scrapping a significant amount of data from the two subreddits, and perform classification modeling and evaluation by splitting them into training and testing sets. The modeling would be done using the training set, whereas the evaluation would be done using the testing set.

"Insufficient facts always invite danger." — Spock

It was found that Multinomial Naïve Bayes is the best model as it achieved 93% of the outcome. This will allow the marketing team to execute better and more informed campaigns to advertise to potential searchers through the Search Engines. In addition, the marketing team would be able to analyze what are the current word trends in Star Wars, and potentially try to pivot the search engine towards Star Trek. Other important aspects of the research include, identifying top active authors from the community for potential collaboration works, identify some of the top words for instagram hastags, and get the sentiments of the general public so that we are able to understand their feedbacks better.

"Change is the essential process of all existence." — Spock

With this systematic and data-driven approach, it will definitely help the team to stay relevant in this ever-evolving technological landscape. And perhaps someday, we might be able to *connect* with Star Wars better... 

"The prejudices people feel about each other disappear when they get to know each other." — Captain Kirk

## Data Collection
---
In the `Scrape and Concat` part of the project, a proper and systematic Data Collection method was developed to perform the following:
- To gather sufficient data for our research.
    - There are a total of approx 6000 posts collected, almost 3,000 posts from each subreddits. 
    - Posts that are blank, removed, or deleted are not in the dataset collected.
- To streamline the data collected.
    - Technically in our NLP project, we only need 2 fields, 
        - target variable, y: the classifications, (aka `subreddit`), startrek = 1, starwars = 0
            - independent variable, X: the posts (aka `self_text`)
- To have a semi-automated way of collecting data as the research still requires some human touch.
    - A generic function was created to have a systematic and smoother data collection from reddit via PRAW.  

- to merge the data collection from the previous notebook and making 2 csv files for two subreddits
    - We will be achiecveing that by concat method.

| fields | description |
| --- | --- |
|subreddit| the name of the subreddit|
|title| the title of the post|
|selftext| the content of the post |
|created_utc| the epoch time|


## Data Cleaning and EDA
---
In the `Part 2: Data Cleaning and EDA` of the research, the following tasks were performed:
- Identified and handled missing values and outliers
- Explored and described some distributions and summary statistics

### Top Active Authors in the Community
These are the authors who have posted a number of posts. Their posts generally receive high score (upvote - downvote) and a high number of comments.
- StarTrek: 'Picard_Indeed', 'R_Jay101', 'GrandAdmiralThrawn4', 'WaveMonkey'
- StarWars: 'DJDMovies', 'YT_DrLiGmA', 'dragonborn_23'
    
### Top 15 Common Words between Star Trek and Star Wars
For Star Trek, it revolves around some of their television series like tng (The Next Generation), ds9 (Deep Science Nine) and picard. Other words like episode, series and season further support this insight.

### Sentiment Analysis
The compound score is a metric that calculates the sum of all the lexicon ratings (pos, neu, neg) which have been normalized between -1 (extreme negative) and +1 (extreme positive). We can see that Star Trek has a more Positive Sentiment as compared to Star Wars.

## Preprocessing and Modeling
---
In the `Part 3: Preprocessing and Modeling` of the project, the following tasks were performed:
- Preprocessing
    - Created "in-house" preprocessor function
        - Remove Identified Words
        - Remove Special Characters
        - Stemming
        - Lemmatizing
    - CountVectorizer
        - GridSearchCV for hyperparameters optimization
    - TfidfVectorizer
        - GridSearchCV for hyperparameters optimization
- Modeling through Pipeline
    - Baseline Accuracy Score 
    - Multinomial Naïve Bayes
        - GridSearchCV for hyperparameters optimization
    - RandomForest
        - GridSearchCV for hyperparameters optimization
- Evaluation
    - The best model would be based on the `Accuracy`, in addition `Sensitivity` would also be referenced.
    
## Conclusion and Recommendations
---

**Model Selection: TF-IDF with Naïve Bayes**

All the models here outperformed the baseline accuracy score of **0.505**. As the focus is on getting as many correct prediction as possible, the Multinomial Naïve Bayes with CountVectorizer has the best predictive performance on the classification problem. On top of that, it has a relatively low False Negative (Type II error) whereby we predicted that post to be Star Wars, but in fact, the post is relating to Star Trek. Hence, we would have to look at the Sensitivity (TP/(TP+FN)), the lower the FN, the higher the Sensitivity. 

Moving forward hrough the research, we will be able to address some other problems such identifying active authors, common words, and performed sentiment analysis. The marketing team and the stakeholders would then be able to perform a more data-driven approach in handling the marketing campaigns. We could potentially include other relevant and similar subreddits into our research, and label all these as binary classification of 0 whereas Star Trek remains as 1. This may expand our modeling capacity. 

In addition, image posts were not taken into account, this could be tapped on given that our current generation usually prefers to post memes instead. Lastly, a more detailed study on the True Negative (TN) would also provide insights for us to pump in to the list of words for the Search Engine, this could potentially direct searchers to our marketing advertisements. 

