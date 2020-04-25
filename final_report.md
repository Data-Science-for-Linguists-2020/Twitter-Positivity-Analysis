# Final Report

## Table of Contents

## Summary

This project looks at Twitter data from the [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) from 2011 and 2019 respectively. It compares and contrasts tweeting habits from both points in time such as content, lexical complexity, tweet length, and tweet sentiment.

## Why Twitter?

Web scraping has always interested me in how much it can tell you about pop culture and human behavior in general. We put so much of ourselves in online spaces, so I wanted to see how online culture, specifically twitter culture, has changed as time has gone on. People often say that social media is a plague, but I have seen a lot of productive discussions to contrast against any percieved negativity as people realize the potential of being this globally connected. I wanted to test the hypothesis that social media has made us less coherrent or willing to start important diaologue. I also wanted to look at the sentiment behind the dialogue and compare it over approximately 8 years. For me personally, 2011 was around the time when I was first expressing myself on the internet, so it is interesting to see how nostalgia colors our view of the past.

## Data

The data for this project comes from a sample of the 2011 and 2019 [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) JSON files, where the top 1% of tweets were scraped from October of 2011 and September of 2019. The data used in the project can be found [here](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/tree/master/data_samples).

Initially, I tried to use the entirety of the dataset which proved to be too much for my computer to process. The original data was about 2.2 GB for 2019 and 0.072 GB for 2011, and was broken up into various files that stored a couple thousand lines of JSON code. Of these files, I took 8 for each year which yielded about 13,000 tweets each.

However, these tweets were still in their rough form. I had a lot of trouble wrangling these datasets and figuring out what direction I should go in with my cleaning. Because I was working with tweets, which heavily featured internet lingo, I had to make sure I wasn't interfering with the integrity of the tweet with my attempts to clean it. My [initial run through](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/data_parsing.ipynb) showed that the unedited dataframes had about 161 columns. They had a plethora of languages, emojis, and hyperlinks. From the numerous attributes of each tweet, I decided to only keep the text, the user's language, and the date the tweet had been created. Then I [pickled]() the data for later use. 

The dataframes for the tweets may have been of a more managable column size, but they also had many non-English languages to deal with. After doing some research, I felt that the [langdetect](https://pypi.org/project/langdetect/) library was a perfect way to quickly classify the tweets into their respective languages. Some of the limitations of language detection included classifying smaller snippets of text, but I decided to still use it because of the volume of data points I had. Even if langdetect made a couple of mistakes, the majority of tweets would still be viable. Additionally, I stripped the text column of its punctuation, hyperlinks, twitter specific words like "retweet", or "rt", and made the text lowercase. Initially I thought keeping the word "retweet" might be able to indicate if there was a conversation taking place, but it ended up messing with the classifier more than providing any valuable input on twitter trends.

After this, I jumped to [building my classifier](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/classifyanalysis.ipynb). It used the open source data from [Sentiment140](http://help.sentiment140.com/for-students), a pre-existing algorithm for sentiment analysis. The classifier data can be found on the website linked above. The data that I took from Sentiment140 already marked their tweets for positive and negative sentiment. Negative sentiment got 0's while positive sentiment got 4's (I changed these labels to "pos" and "neg"). Using a pipeline with the tfidf vectorizer, I built a multinomial naive bayes classifier with an accuracy score of about 77%. I felt that this was sufficient enough to begin classifying my main dataset. 

In addition to running both tweets2011 and tweets2019 dataframes through the sentiment classifier, I created unigrams, bigrams, and trigrams of the text in each tweet in order to better understand the context behind the sentiment analysis. I also documented the tweet length (number of words per tweet), and average word length. 

My final dataframes were 5343 lines for 2011 and 4932 lines for 2019. 

## Analysis

### Lexical Complexity

The first analysis I performed on my data was to get a general sense of how tweets were written. This included word length, tweet length, and TTR. 

Let's start with word length. Initially, I hypothesized that tweets from today would be more verbose than tweets from 8 years ago because of more sophisticated use of the platform, and for added features like [tweet threads](https://business.twitter.com/en/blog/How-Tweet-threads.html). The data, however, completely contradicted my point.

<chart here>

Based on this boxplot, both the averages and the relative max and min values are in the same range for tweets from 2011 and tweets from 2019. The average tweet length was 11.37 words long in 2011, and 12.65 words long in 2019. While it is true that average tweet length has increased since 2011, it is by such a tiny amount that I feel like the difference is negligible. Futhermore, the fact that the max and min word count are also within 1 space of eachother makes it clear that this is not due to any outliers. 





