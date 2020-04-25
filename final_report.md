# Final Report

## Table of Contents

  * [Summary](#summary)
  * [Why Twitter?](#why-twitter-)
  * [Data](#data)
    + [Cleaning](#cleaning)
    + [Classifier](#classifier)
  * [Analysis](#analysis)
    + [Lexical Complexity](#lexical-complexity)
    + [Sentiment](#sentiment)
  * [Polarity values for 2011](#polarity-values-for-2011)
  * [Polarity values for 2019](#polarity-values-for-2019)
  * [Conclusions](#conclusions)
  * [Looking back...](#looking-back)

## Summary

This project looks at Twitter data from the [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) from 2011 and 2019 respectively. It compares and contrasts tweeting habits from both points in time such as content, lexical complexity, tweet length, and tweet sentiment.

My hypothesis is that tweets from 2019 have gotten more streamlined in topic and more lexically complex. I also believe that they have a more negative overall sentiment as a result of the focus on current events. 

Here is my [final notebook](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/finalnb.ipynb) which picks up after the data has been parsed and the classifier has been built.

## Why Twitter?

Web scraping has always interested me in how much it can tell you about pop culture and human behavior in general. We put so much of ourselves in online spaces, so I wanted to see how online culture, specifically twitter culture, has changed as time has gone on. People often say that social media is a plague, but I have seen a lot of productive discussions to contrast against any percieved negativity as people realize the potential of being this globally connected. I wanted to test the hypothesis that social media has made us less coherrent or willing to start important diaologue. I also wanted to look at the sentiment behind the dialogue and compare it over approximately 8 years. For me personally, 2011 was around the time when I was first expressing myself on the internet, so it is interesting to see how nostalgia colors our view of the past.

## Data

The data for this project comes from a sample of the 2011 and 2019 [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) JSON files, where the top 1% of tweets were scraped from October of 2011 and September of 2019. The data used in the project can be found [here](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/tree/master/data_samples).

### Cleaning

Initially, I tried to use the entirety of the dataset which proved to be too much for my computer to process. The original data was about 2.2 GB for 2019 and 0.072 GB for 2011, and was broken up into various files that stored a couple thousand lines of JSON code. Of these files, I took 8 for each year which yielded about 13,000 tweets each.

However, these tweets were still in their rough form. I had a lot of trouble wrangling these datasets and figuring out what direction I should go in with my cleaning. Because I was working with tweets, which heavily featured internet lingo, I had to make sure I wasn't interfering with the integrity of the tweet with my attempts to clean it. My [initial run through](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/data_parsing.ipynb) showed that the unedited dataframes had about 161 columns. They had a plethora of languages, emojis, and hyperlinks. From the numerous attributes of each tweet, I decided to only keep the text, the user's language, and the date the tweet had been created. Then I pickled the data for later use. 

The dataframes for the tweets may have been of a more managable column size, but they also had many non-English languages to deal with. After doing some research, I felt that the [langdetect](https://pypi.org/project/langdetect/) library was a perfect way to quickly classify the tweets into their respective languages. Some of the limitations of language detection included classifying smaller snippets of text, but I decided to still use it because of the volume of data points I had. Even if langdetect made a couple of mistakes, the majority of tweets would still be viable. Additionally, I stripped the text column of its punctuation, hyperlinks, twitter specific words like "retweet", or "rt", and made the text lowercase. Initially I thought keeping the word "retweet" might be able to indicate if there was a conversation taking place, but it ended up messing with the classifier more than providing any valuable input on twitter trends.

### Classifier

After this, I jumped to [building my classifier](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/classifyanalysis.ipynb). It used the open source data from [Sentiment140](http://help.sentiment140.com/for-students), a pre-existing algorithm for sentiment analysis. The classifier data can be found on the website linked above. The data that I took from Sentiment140 already marked their tweets for positive and negative sentiment. Negative sentiment got 0's while positive sentiment got 4's (I changed these labels to "pos" and "neg"). Using a pipeline with the tfidf vectorizer, I built a multinomial naive bayes classifier with an accuracy score of about 77%. I felt that this was sufficient enough to begin classifying my main dataset. 

In addition to running both tweets2011 and tweets2019 dataframes through the sentiment classifier, I created unigrams, bigrams, and trigrams of the text in each tweet in order to better understand the context behind the sentiment analysis. I also documented the tweet length (number of words per tweet), and average word length. 

My final dataframes were 5343 lines for 2011 and 4932 lines for 2019. 

## Analysis

### Lexical Complexity

The first analysis I performed on my data was to get a general sense of how tweets were written. This included word length, tweet length, and TTR. 

Let's start with word length. Initially, I hypothesized that tweets from today would be more verbose than tweets from 8 years ago because of more sophisticated use of the platform, and for added features like [tweet threads](https://business.twitter.com/en/blog/How-Tweet-threads.html). The data, however, completely contradicted my point.

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/tweetlen.png?raw=true "Tweet Length Box Plot")

Based on this boxplot, both the averages and the relative max and min values are in the same range for tweets from 2011 and tweets from 2019. The average tweet length was 11.37 words long in 2011, and 12.65 words long in 2019. While it is true that average tweet length has increased since 2011, it is by such a tiny amount that I feel like the difference is negligible. Futhermore, the fact that the max and min word count are also within 1 space of eachother makes it clear that this is not due to any outliers. 

This result does make sense to some degree. Since twitter has a character count users are probably confined to those limitations, making the average word count more or less consistent. 

The average word length tells a slightly different story though.

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/wordlen.png "Word Length Box Plot")

This time, even though the averages are in the same range, the max word length for 2011 is a whopping 35 characters long. Why is that? Surely users 8 years ago weren't sprinking lengthy vocab into their already limited tweeting space? Taking a look at some examples of lengthy tweets we can see exactly why this result occured. 


![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/longword.PNG?raw=true "Long Text")

The highlighted portion of this dataframe shows a phenomenon common on the internet during the early 2010's. Users would typelikethisinordertoconveyafrantictone, like everything was being said in one breath. This spaceless typing is not uncommon in 2019, however it seems to be relagated to hashtags rather than full sentences. 


Another measure used on the data was TTR. This showed whether the tweets from either era had any lexical complexity. My hypothesis was similar to the one mentioned earlier-- I thought that 2019's tweets would have a lower TTR, thus a more lexically complex corpus. 

Here is the result of calculating TTR for unigrams:

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/unigrams.png "TTR for unigrams")

As I suspected, 2019's TTR was higher than 2011. Type-token ratio for 2011 was 0.20, while the ratio for 2019 was 0.23. It seems that 2019 has a slightly more diverse vocabulary. These word clouds might better demonstrate that effect:

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/unigram11.png "2011 unigram cloud")
Word Cloud for 2011 unigrams

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/unigram19.png "2019 unigram cloud")
Word Cloud for 2019 unigrams

The larger the word, the more it appears in the corpus. As you can see, the cloud from 2011 unigrams has very large and prominent words, indicating that these keep repeating. The 2019 cloud has many same-sized words (and an example of the long hashtag format) indicating more lexical diversity. 

We can perform this same test with bigrams and trigrams in order to see which phrases appear to pop up often.

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/bigram11.png "2011 unigram cloud")
Word Cloud for 2011 bigrams

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/bigram19.png "2019 unigram cloud")
Word Cloud for 2019 bigrams


We see the same result repeated, with larger words in 2011 and same-sized words in 2019.


![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/trigram11.png "2011 unigram cloud")
Word Cloud for 2011 trigrams

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/trigram19.png "2019 unigram cloud")
Word Cloud for 2019 trigrams

And repeated again. 


Interestingly, many of these 2011 word clouds have more generic, common phrases like "i love you" or "i want to", but the 2019 word clouds have words like "1 vote" or "bbmastopsocial" or "high school college" indicating a more sophisticated and topical dialogue taking place among the 2019 tweets. They use more hastags over all-- so much so that the most frequent unigram is actually a hashtag. This indicates that users engage more with current events through tweets. 

### Sentiment

We can also figure out which topics are percieved positively or negatively. 

First, lets look at some stats on the entirety of the corpus: This is how the classified tweets stacked up. 

Polarity values for 2011
---
neg  |  2861
--- | ---
pos  |  2482

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/pie11.png "2011 pie chart")

Polarity values for 2019
---
neg  |  2632
--- | ---
pos  |  2300

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/pi19.png "2019 pie chart")

A pretty even split for both of the dataframes! Negative tweets beat the positive ones by just a hair. Let's see why?

I used trigrams and divided them by negative and positive sentiment. These clouds will how three word phrases present in each category of tweet. 

2011:

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/pos11tri.png "2011 pie chart")

2019:

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/pos19tri.png "2011 pie chart")

The 2019 cloud seems to be nothing but the "reply 1 vote" trigram and variations of. Very focused on the current event and hashtag of the moment. The 2011 cloud looks more littered with positivity, the strongest phrase being "I love you". The word love actually does appear a lot more often overall.


The negative word clouds don't really have anything striking about them:


2011:

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/neg11tri.png "2011 pie chart")

2019:

![alt text](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/images/neg19tri.png "2011 pie chart")

The words that appear are considerably smaller than the giant "i love you" from the positive cloud. In the 2011 cloud, "you're single focus on being a better you" was a popular hashtag or topic of conversation that repeated itself through many tweets. This sentiment seems to be slightly positive, but implies that the starting point for the reader is not a "better" version of themselves, so there might be additional negative dialogue in the body of the tweets. It seems like there isn't much substance to the negative tweets from 2011. This implies that tweets from 2011 were more concrete in their positivity, repeating certain words and phrases, where as the negative tweets were not unified in any way. In the 2019 cloud, all of the words being roughly the same size shows that there was no common topic of negativity among the tweets. The phrases range from comments on followers, to conversations about school, to opinions air travel. There are a few automated messages sprinkled in there as well.

Like the 2011 cloud, the words are small in the 2019 cloud, however, their uniformity could suggest that there were more negative tweets in general that year, where as the 2011 tweets had a certain topic that was slightly bigger than the others.  Overall, the negative tweets are not as unified as the positive ones. 

## Conclusions

The results somewhat supported my hypothesis. I thought that the tweets from 2019 would lean more towards current events and be more sophisticated. I also hypothesized that they would yield a negative sentiment overall. It seems the data showed signs of users engaging more with current events and hashtags. Some common phrases engaged with the BBMA awards, the billboard music awards, mentions of voting, and mentions of high school and college, which all point to a more topic driven discourse. The tweets from 2011 however, exude more "positivity" in the sense that they have a stronger inclination to use positively correlated words and phrases like "i love you", "check it out", "i want to", etc. The positive word cloud for 2019 has "vote 1 reply" as the most prominent positively tagged phrase, which isn't actually a phrase that we would associate with being overly positive. The hypothesis was disproven, however, in the assumption that the tweets of 2019 would be more "sophisticated". The average word length and average tweet length was practically the same for both years, with the only major difference being a result of the typing styles of the time. The type-token ratio to show lexical diversity also only had marginal results, with a difference of only 0.03. Both years were evenly lexically diverse. 

## Looking back...

This project was definitely intimidating for me due to the unwieldy size and makeup of the data. However, if I could do it over again I would try to pick tweets that were more focused on a specific topic rather than a mixed bag. I would also have liked to pay more attention to internet lingo while cleaning the data, but since I was just learning how to scrape tweets, I felt like that was something to tackle for the next round. 

The biggest struggle was in finding data and then cleaning data. I had to make sure my tokens would be recognizable enough to the classifier so that certain abbreviations that were made due to the medium being online and the character limit requiring some creative spellings wouldn't be overlooked. 

I would also love to get into analysis earlier than I did so that I could really dig much deeper than I was able to here.
