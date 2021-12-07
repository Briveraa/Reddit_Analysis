# Reddit Analysis Project
![](https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/healthy-food-clean-eating-selection-royalty-free-image-854725372-1538493619.jpg)
---
### Description
The goal of this project is to create a model that can predict which posts came from a given subreddit. For this project I used the plant based subreddit and nutrition subreddit to analyze. 


### Data 
I pulled about 1600 posts from the plant based subreddit and choose to drop the duplicates rows. For the nutrition subreddit I pulled about 1900 posts and also droped the duplicate rows. Below is a data dictionary for the dataframes I created in this project. 

| Name        | Type    | Dataset                   | Description                                                                                                                       |
|-------------|---------|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| plant_based | int/obj | subreddits                | Data frame of plant based subreddit submissions                                                                                   |
| df_1        | obj     | plant_based               | Important features from the plant_based data frame. Contains id, subreddit, selftext, and title. Contains 1653 rows and 4 columns |
| nutrition   | int/obj | subreddits                | Data frame of nutrition subreddit submissions                                                                                     |
| df_2        | obj     | nutrition                 | Important features from the nutrition data frame. Contains id, subreddit, selftext, and title. Contains 1916 rows and 4 columns   |
| combined_df | int/obj | plant_based and nutrition | Contains id, subreddit, selftext, title, label.                                                   |
| explore     | obj     | combined_df               | Contains label and selftext from the combined df_1 and df_2                                                                     |


### Model
I began modeling with the clean data, starting by first creating a pipeline that consisted of the count vectorizer as my transformer and random forest classifier as my estimator. I then used a grid search to search over different parameters (a total of 8 parameters each with a list of values to try out) for both the count vectorizer and random forest classifier. After running the random forest classifier I chose to use the voting classifier with three different estimators: logistic regression, random forest classifier, and SVM (support vector machine). This voting classifier trains on an ensemble of models; it essentially aggregates the findings of each classifier passed into the voting classifier and predicts the output class based on the highest majority. 


| Model                    | Train Score: | Test Score: |
|--------------------------|--------------|-------------|
| Random forest classifier | 0.99         | 0.79        |
| Voting classifier        | 0.97         | 0.81        |                  

#### Conclusion
Based on the scores above the voting classifier gave the best test score-- this model does high varience though. It seems that peanut butter is one of the most frequent words in both subreddits. I think more analysis such as polarity analysis needs to be done on those specific posts that mention peanut butter in order to tell if these people are talking about in a positive or negative way? For this to be more informative, I would have to do some more cleaning of the posts in the plant based diet subreddits. I think adding more data would also help in addition to creating a customized list of stop words. 
