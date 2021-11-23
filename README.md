# Twitter Classification project

## Introduction:

A web scraping project with classification problem prediction. Two twitters that has high focus on mental well being and self love. One globally recognized throughout various religious groups the other well-known in the region. In this project I will use the twitter api to scrape data from twitter and run a few classification models then choose the best.

## The Process:

1. Problem Statement
2. Data Collection
3. Data Cleaning 
4. Preprocessing & EDA
5. Modelling & Evaluation
6. Conclusion and Suggestions

----------------------------

## 1. Problem Statement: 
- Given a random tweet, assign accordingly to the correct twitter account based on similar occuring words.
- What are the most repeated words in each tweet.
- What is the average length of words for each tweet.

### 2. Data Collection:

Scrap two twitter accounts: Mufti Menk & Mizi Wahid, using twitter scrapper and import to csv file.

A total collection of 1798 tweets(incl. retweets) were scraped from both accounts.


### 3. Data Cleaning:

Series of cleaning done:
1. Regex (String to lower case, remove non words characters and numbers (punctuation, curly brackets etc))
2. Lemmatize
3. Tokenize
4. Remove stopwords


### 4. Pre-processing and EDA

Final results for both accounts:

|Twitter Account| Tweets|
|---------------|-------|
|Mufti Menk| 896 |
|Mizi Wahid| 657 |


Basic EDA:

|Item               | Mufti Menk | Mizi Wahid |
|-------------------|------------|------------|
|Average length/tweet| 269.25    | 196.03     |
|Longest tweet length| 293       | 290        |
|Average word count/tweet| 52.13 | 36.98      |
|Maximum word count/tweet| 64    | 63         |
 
![muftimenkwordcount](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/blob/main/images/muftimenk%20word%20count.png)
![miziwahidwordcount](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/blob/main/images/miziwahid%20word%20count.png)

### 5. Modelling and Evaluation

Data distribution is quite balanced:

-Mufti Menk (0): 0.576948
-Mizi Wahid (1): 0.423052

Some of the top occuring words in each account:

![muftimenktopword](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/blob/main/images/topword%20muftimenk.png)
![miziwahidtopword](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/blob/main/images/topwords%20miziwahid.png)

The choice of repeated words found in each accounts shows the word 'God' often. This shows how important the presence of God in their way of preaching and keeping a positive well being.

For this project I ran two models Random Forest(rf) and Multinomial Naive Bayes(nb) after running CountVectorizer(cvec) in the pipeline.

- Best parameters for the first model: cvec__max_df: 0.75, cvec__max_features: 170, cvec__min_df: 0.1, cvec__ngram_range: (1, 1), rf__max_depth: 2
- Best parameters for the second model: cvec__max_df: 0.75, cvec__max_features: 170, cvec__min_df: 0.05, cvec__ngram_range: (1, 1), nb__alpha: 0.3

Summary table results:

|Model name| Train_AUC | Test_AUC | Precision | Recall | F1_Score |
| -------- | --------- | -------- | --------- | ------ | -------- |
|Random Forest | 0.92 | 0.91 | 0.80 | 0.81 | 0.80 |
|Multinomial NB | 0.90 | 0.87 | 0.78 | 0.58 | 0.67 |

By using Logistic Regression to look at the best predicting words for each twitter account as follows:

![muftimenkbestpredict](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/blob/main/images/bestpredictingwords%20muftimenk.png)
![miziwahidbestpredict](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/blob/main/images/bestpredictingwords%20miziwahid.png)


### 6. Conclusion and Suggestions

In conclusion: Random Forest Classifier performed better than Multinomial Naive Bayes.

Top 5 words best predict each account:

Mufti Menk:
1. Almighty
2. aremember
3. life
4. let
5. keep

Mizi Wahid:
1. god
2. wahid
3. love
4. new
5. Allah


Just like previously mentioned the word God is highly repeated in both accounts. Being the subject matter of their tweets mostly revolve around self-love and mental well being you can see that the word 'love', 'remember', 'let' as in let go of the negativity, 'keep' as in keep hold of the good things in life would predict the best for each account.

#### Suggestions to improve:

1. Additional words can be added into the list of stopwords, for example the words that has high frequency in both twitters.
2. Further improve on lemmatizing and tokenizing
3. Experiment with other types of algorithms and ensemble methods such as Boosting, Bagging etc.
