# Subreddit Classification

Author: Clement Ow

### Contents:
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Data Dictionary](#Data-Dictionary)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)

## Problem Statement

Assuming the production instance of Reddit went down recently which led to many posts getting stuck in the queue to be processed. Unfortunately, at the juncture when the Subreddit tag was to be tagged to the post, the system went down and thus was not able to tag the post successfully. The aim of this project is to then classify a post back into the correct Subreddit in the most accurate manner by using machine learning and Natural Language Processing (NLP) techniques. This will be a binary classification problem consisting of posts from two Subreddits, _r/MentalHealth_ and _r/Psychology_.

_r/MentalHealth_ and _r/Psychology_ were chosen because it is neither too similar nor too different. There are overlapping topics and we can see if the accuracy of the classification is indeed going to be good or bad.

A few machine learning models will be going through supervised learning to be trained on existing data from each Subreddit. The model with the best accuracy will be the model of choice for this classification problem. This model can continue to train on new data for new posts to enhance its accuracy.

## Executive Summary

In recent years, there has been many cases of suicide rates increasing, mental health disorders skyrocketing and hitting millions of people in the world. Understanding the texts through NLP of two subreddits _r/MentalHealth_ and _r/Psychology_ are good starting points for a classification task.

Data is gathered by scrapping posts from the two popular subreddits and then training the model on 75% of the data and subsequently the other 25% as the unseen test set to evaluate the model performance. The models used will be:
- Logistic Regression
- Naive-Bayes Classifier
- Random Forest Classifier

After the training and testing phases, Logistic Regression performed the best in terms of the accuracy score. But in terms of the interpretability of the features and that it includes nearby words as well, **Naive-Bayes Classifer** is ultimately the model of choice for this classification problem. Misclassification rate is also relatively low and they are mostly due to uncontrollable factors wherein the posts that usually appears in _r/Psychology_ appeared in _r/MentalHealth_ and vice versa.

However, to truly increase the performance of the model, further research on understanding texts through linguistic features and contextualisation would need to be performed. Identifying and inputting more features into the model can also aid in increasing accuracy scores as well. Ultimately, to further tune the model we have to use an interpretable model in either Logistic Regression or Naive-Bayes Classifier to read the results to ensure it makes sense apart from just the accuracy scores.    

## Data Dictionary

| Field     | Type   | Description                                                         |
|-----------|--------|---------------------------------------------------------------------|
| title_txt | string | The title and selftext of reddit post                               |
| class     | int    | class = 1 refers to r/MentalHealth, class = 0 refers to r/Psychology |

## Conclusions and Recommendations

### Model Comparison

| Model               | Training Score | Test Score | ROC AUC Score |
|---------------------|----------------|------------|---------------|
| Logistic Regression | 0.999          | 0.948      | 0.98          |
| Naive-Bayes         | 0.962          | 0.946      | 0.985         |
| Random Forest       | 1.0            | 0.944      | 0.99          |

The best model in terms of test score will be the Logistic Regression model with a relatively good ROC AUC score of 0.98 which is pretty close to the other models.

However, the ultimate winner would be the __Naive-Bayes model__. Its test score is just shy of 0.02 at 0.946 which is pretty decent and this model generalises well and do not overfit the training data as compared to the others. One important point is that it greatly increases model result interpretability by clearly specifying the top features by subreddit. It recognised that some of the bigrams in each class are ranked higher in each class which is a further plus point. Furthermore, its ROC AUC score is slightly higher than that of Logistic Regression indicating that the two classes are quite well split.

### Misclassifications

The misclassification rate is relatively low at 26-27 out of close to 2000 posts depending on the model used.

Looking into some of them, they were misclassified due to the fact that the post was quite similar to redditors who post on the other subreddit. For example, in a False Negative case (when prediction was _r/Psychology_):
> "U.S. Suicide Rates Are the Highest They've Been Since World War II \[U.S. suicide rates\] are at their highest since World War II, according to federal data‚and the opioid crisis, widespread social media use and high rates of stress may be among the myriad contributing factors.".

Such a post usually appears on _r/Psychology_ and hence was misclassified as such.

For the False Positive case (when the prediction was _r/MentalHealth_):
>"In light of the very tragic Connecticut Elementary School shootings, everyone is now bringing up gun control again. What no one is talking about (and never seems to talk about) is helping to increase mental health healthcare in the country.  And it's pissing me off.".

This post has alot of the author's feelings in it and thus makes the machine think that it is under _r/MentalHealth_ where redditors mostly pour our their feelings into their posts.

There tends to be some anomalies as to the post structure and subjectivity that is posted to both subreddits. Since it is user driven community and as long as it does not flout any of the community guidelines the moderators will just let the post be.

### Assumptions

- We are assuming that the models will treat each word as an independent variable.
- The bag of words approach is a good indicator for prediction.  
- We do not want to penalise document frequency as we are not doing Information Retrieval tasks.

### Recommendations

Looking at the context of words of how it is being used and linguistic features will be a better way of understanding text from a human. Of course, understanding sarcasm is one of the ongoing research which will help immensely in machine interpretability and higher accuracy rates.

Sentiment analysis can be one interesting feature to input into the model to see if it will improve performance since these are subreddits that can potentially be very personal.

Additionally, more features like length of posts can be identified and input into the model to see if it will increase accuracy scores.
