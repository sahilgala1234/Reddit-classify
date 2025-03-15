# Subreddit Classification

### Contents:
- [Problem Statement](#problem-statement)
- [Executive Summary](#executive-summary)
- [Data Dictionary](#data-dictionary)
- [Conclusions and Recommendations](#conclusions-and-recommendations)

## Problem Statement

Recently, Reddit experienced a system outage that caused many posts to be stuck in the processing queue. Specifically, the system failed at the stage where Subreddit tags were being assigned to posts, leaving them untagged. The goal of this project is to accurately classify these posts back into their correct Subreddits using machine learning and Natural Language Processing (NLP) techniques. This will be a binary classification task involving posts from two Subreddits: _r/MentalHealth_ and _r/Psychology_.

These Subreddits were chosen because they share overlapping topics but are distinct enough to pose a meaningful classification challenge. By evaluating the accuracy of the classification, we can determine how well the model performs in distinguishing between the two.

Several machine learning models will be trained using supervised learning on existing data from each Subreddit. The model with the highest accuracy will be selected for this classification task. This model can then be continuously updated with new data to improve its performance over time.

## Executive Summary

In recent years, there has been a significant rise in mental health issues, with increasing rates of suicide and mental health disorders affecting millions worldwide. Analyzing the text from two Subreddits, _r/MentalHealth_ and _r/Psychology_, using NLP techniques provides a valuable opportunity for a classification task.

Data was collected by scraping posts from these two Subreddits. The dataset was split, with 75% used for training the models and the remaining 25% reserved as a test set to evaluate performance. The following models were used:
- Logistic Regression
- Naive-Bayes Classifier
- Random Forest Classifier

After training and testing, Logistic Regression achieved the highest accuracy score. However, considering interpretability and the ability to capture contextual relationships between words, the **Naive-Bayes Classifier** emerged as the preferred model for this classification problem. The misclassification rate was relatively low, with most errors arising from posts that could reasonably belong to either Subreddit.

To further enhance model performance, future work could focus on incorporating linguistic features and contextual understanding of text. Adding more features, such as sentiment analysis or post length, could also improve accuracy. Ultimately, an interpretable model like Logistic Regression or Naive-Bayes is essential for ensuring that the results are not only accurate but also meaningful.

## Data Dictionary

| Field     | Type   | Description                                                         |
|-----------|--------|---------------------------------------------------------------------|
| title_txt | string | The title and selftext of a Reddit post                             |
| class     | int    | class = 1 refers to _r/MentalHealth_, class = 0 refers to _r/Psychology_ |

## Conclusions and Recommendations

### Model Comparison

| Model               | Training Score | Test Score | ROC AUC Score |
|---------------------|----------------|------------|---------------|
| Logistic Regression | 0.999          | 0.948      | 0.98          |
| Naive-Bayes         | 0.962          | 0.946      | 0.985         |
| Random Forest       | 1.0            | 0.944      | 0.99          |

Logistic Regression achieved the highest test score and a strong ROC AUC score of 0.98, making it the best-performing model in terms of accuracy. However, the **Naive-Bayes Classifier** is the preferred choice due to its balance of performance and interpretability. With a test score of 0.946 and a slightly higher ROC AUC score of 0.985, Naive-Bayes generalizes well without overfitting. Additionally, it provides clear insights into the most important features for each Subreddit, including bigrams that are highly relevant to each class.

### Misclassifications

The misclassification rate was relatively low, with 26-27 errors out of nearly 2000 posts, depending on the model used. 

For example, a False Negative case (predicted as _r/Psychology_ but actually from _r/MentalHealth_):
> "U.S. Suicide Rates Are the Highest They've Been Since World War II \[U.S. suicide rates\] are at their highest since World War II, according to federal data‚and the opioid crisis, widespread social media use, and high rates of stress may be among the myriad contributing factors."

This post, which discusses suicide rates and contributing factors, is more typical of _r/Psychology_, leading to its misclassification.

In a False Positive case (predicted as _r/MentalHealth_ but actually from _r/Psychology_):
> "In light of the very tragic Connecticut Elementary School shootings, everyone is now bringing up gun control again. What no one is talking about (and never seems to talk about) is helping to increase mental health healthcare in the country. And it's pissing me off."

This post, which expresses strong personal emotions, was misclassified as belonging to _r/MentalHealth_.

These misclassifications highlight the overlap in topics and the subjective nature of posts in both Subreddits. Since Reddit is a user-driven platform, posts often reflect the personal perspectives of their authors, leading to some ambiguity in classification.

### Assumptions

- Each word is treated as an independent variable by the models.
- The bag-of-words approach is a suitable method for prediction.
- Document frequency is not penalized, as this is not an Information Retrieval task.

### Recommendations

To improve model performance, future efforts could focus on incorporating contextual understanding of words and linguistic features. Sentiment analysis could be a valuable addition, given the personal and emotional nature of many posts in these Subreddits. Additionally, features such as post length or the presence of specific keywords could be explored to enhance accuracy.

Ultimately, the goal is to develop a model that not only achieves high accuracy but also provides interpretable and meaningful results. By leveraging interpretable models like Logistic Regression or Naive-Bayes, we can ensure that the classification outcomes align with human understanding and expectations.
