# Summary

In this article I will explain in detail on how I worked on the twitter classification project.

# Introduction

Mental issue has been a big topic in the recent years and has burst even more after the recent covid pandemic with the closing of borders, lockdown situation and what not.
This project is part of NLP projects and using classification algorithms to predict the twitters to the correct account holder. And the twitter I chose are both whom I really admire especially in the areas of mental well being and self love. Before I go further let me breakdown the points of this article and we'll go through it one by one.

Content:

1. Twitter Scrapping
2. Natural Language Processing
3. Classification Modelling


## 1. Twitter Scrapping (Tweepy)

This is the one that took the most part of my the project but it was worthwhile. To begin, there are a few different API that will scrape tweets from twitters. From what I have explored Tweepy has been the most suitable for me. So let's get to it.

### Step 1: Get a developer account from twitter

In order to receive credentials, you must apply to become a Twitter developer here. This does require that you have a Twitter account. The application will ask various questions about what sort of work you want to do. Don’t fret, these details don’t have to be extensive, and the process is relatively easy. [Apply here](https://developer.twitter.com/en/docs/twitter-api)

![Twitter Developer Landing Page](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/blob/gh-pages/pages_images/Twitter%20Developer%20landing%20page.png)

### Step 2: Get credentials

In order to get your credentials: API key, API key secret, Access token, Access token secret, you wil have to create a project and an app from the project within your developer account. Make sure to copy and paste it somewhere to use it for scraping because if you need to look at it again you will have to regenerate which is kind of a hassale.

### Step 3: Install Tweepy

If you have not installed it yet then you may do so with the following codes:

```markdown

pip install tweepy

pip3 install tweepy

```

If you prefer to install in your jupyter notebook like I did, use the former. You may also install it via the command prompt this works for python 3. The tweepy version I am currently using is 4.1.0.


### Step 4: 

```markdown

import tweepy

auth = tweepy.OAuthHandler(API key, 
                           API key secret)
auth.set_access_token(Access Token,
                      Access Token Secret)
                      
api = tweepy.API(auth)                      
                      
```

Create a list of timeline_ids to use to fetch the correct timeline for a twitter account:

```markdown

user_name = ['muftimenk', 'mizi_wahid']
counter = 0 
timeline_ids = {} 
start_time = datetime.now() 
for i in user_name:
    user_object = api.get_user(id = i) 
    print("User screen name is: ", user_object.screen_name) 
    print("Users id in twitter db is: ", user_object.id) 
    print("Users info shown on twitter is: ", user_object.name) 
    print("User was created at: ", user_object.created_at) 
    user_id = user_object.id
    print('-------\n')
    timeline_ids[user_id] = list()
print(timeline_ids)

```

Here we need to use a Cursor, What is Cursor doing it is actually ....

```markdown

for i in timeline_ids: #to iterate through each account
    for status in tweepy.Cursor(api.user_timeline, user_id = i).items(1000): # scraping the status id and insert it to a list
    # process status here 
        timeline_ids[i].append(status.id)
        counter += 1 
print(timeline_ids)

```

Why I didn't scrape directly it is because twitter has a limit of how much tweets you can scrape within a 15 min period which is 

So with this method you can use a crawling method to automatic put a timer of 15 min before continue to scrape the next batch and so on.

There are a few params you can use to get what you want, you may look at the documentation [here](https://www.documentation.com)

```markdown

# Set looping params
start_time = datetime.now() 
raw_tweets = list()
count = 0
for key, values in timeline_ids.items():
    for i in values:
        try:
            res = api.get_status(id = i, tweet_mode = "extended") 
            raw_tweets.append({
                           "username": key,
                           "accident_id": i,
                           "created_at": res.created_at,
                           "text": res.full_text,
                           "len": len(res.full_text),
                           "source": res.source,
                           #"likes": np.array([res.favourite_count for tweet in res]),
                           #"retweets": np.array([res.retweet_count for tweet in res])
                                }) 
            #end_time = datetime.now()
            #start_time = datetime.now()
            #print(end_time - start_time)
            #t.sleep(60 * 15) 
            del res
            print(count)
            count += 1 # check the number of requests
        except tweepy.TooManyRequests as r:
            print(f'{count}: Rate limit error exceed 490 requests')
    end_time = datetime.now()
    print(end_time - start_time)
    start_time = datetime.now()
    t.sleep(60 * 15)
    end_time = datetime.now()
    print(end_time - start_time)
end_time = datetime.now()
print(end_time - start_time)
print(raw_tweets)

```

After that is done I double checked on the len

```markdown

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Mr-Ahmad-Khalil/Twitter_Classification/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Resources:

1. [How to Scrape tweets from Twitter](https://towardsdatascience.com/how-to-scrape-tweets-from-twitter-59287e20f0f1) that explains more. I used the tweepy for scraping.

