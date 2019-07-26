# Web Scraping and Topic Modelling
> Author: Shruthi
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# PROJECT 
Problem Statement: 

Model a binary classifier to execute classification

Modus Operandi Overview:

Posts are collected from two sub-reddits: Sports and Politics. This is done by sending a request to reddit's api. Since, the api only allows 25 posts per request a for loop is run to collect over 1000 posts. Once 1000 posts are collected for each of the sub-reddits, all the text in every post is going to be count vectorized which will then be the input into the classifiers. A Naive-Bayes classifier is used to train the model and a logistic regression classifier is used to compare the performance.

Process Highlights:

* Collecting Data:
  * Sending a request to reddit's api to collect one page of posts from "https://www.reddit.com/r/sports.json" 
    and "https://www.reddit.com/r/politics.json" . Then creating a for loop to collect posts ending from each page's js['data']['after']
  * Constructing a dataframe for each of the sub-reddit's posts and then combining the two dataframes

* EDA:
  * Feature construction from the given data frame; 
    features chosen were: "data.title","data.author","data.domain","data.name","data.subreddit","data.subreddit_id","data.url"
  * No null values
  * Feature Engineering
    Creating a new coloumns called "Sports or Politics": which is a mapped function of "data.sub-reddit": If the sub-reddit belongs to 
    politics the mapped value is 1 else it is 0.
    As you will see, This will be our target feature.
  
 * Modelling:
   * A TfidfVectorizer is fit to our training set of "data.title" of our combined data frame. The count vectorizer is initialized to          have max-features of 1000 with the imported library of stop words in english.
     The shape of the count-vectorized dataset is 1477,1000
   *  A multi-nominal Naive Bayes model is initialized because we have integer counts as our target column and it works well with
      TfidfVectorizers
   * Logistic Regression is initialized also because our target column is a 1 or 0
   
  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  # Results:
  
  > For the Naive Bayes Model:
  
  Accuracy: 96.9 %
  
  True Negatives  | 240  | 
  False Positives | 6    |
  False Negatives | 4    |
  True Positives  | 243  |
 
   > For Logistic Regression:
   
   Accuracy: 96.7%
   
   True Negatives   | 246 |
   False Positives  | 0   |
   False Negatives  | 14  |
   True Positives   | 233 |
   
   -------------------------------------------------------------------------------------------------------------------------------------
   
   # Conclusion:
   
   The Logistic Regression has performed better at differentiating the texts over the Naive Bayes model because of the lower number of 
   False Positives and False Negatives it has compared to the Naive Bayes model's. The two sub-reddit's are distinctly different 
   and hence the model's are able to perform so well.
   
   ## Word Clouds
   
   > Politics Wordcloud
   ![picture alt](https://github.com/shruthis-work/Topic-Modelling/blob/master/Politics_wordcloud.png "Politics Wordcloud")
   
   > Sports Word Cloud
   ![picture alt](https://github.com/shruthis-work/Topic-Modelling/blob/master/Sports_wordcloud.png "Sports Wordcloud")
   
   # Recommendations:
   
   The data keeps getting updated everytime the website is refreshed, hence everytime the request is made a new dataset is obtained.        This makes a steady training set unavailable to train the models and it affects the words the count vectorizer is fit to. This          affects the performance of the models. A constant backed up data on the api would improve the fit of the count-vectorizer and hence      train a steadier classifier. Never the less, the word clouds prove that the words have been clearly differentiated.
   
   # General Comments:
   This model is built to differentiate whether a post belongs to the Sports topic or the politics topic and has achieved that.
   According to the Word Clouds, the current hot-topic in the sports sub-reddit is the Cricket World Cup. The current hot-topic in the      politics sub-reddit is Trump as usual, Republicans vs Democrats so a conclusion would be that American Politics does really affect      the world.
