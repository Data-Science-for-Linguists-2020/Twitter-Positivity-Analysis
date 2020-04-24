# Final Report

## Table of Contents

## Summary

This project looks at Twitter data from the [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) from 2011 and 2019 respectively. It compares and contrasts tweeting habits from both points in time such as content, lexical complexity, tweet length, and tweet sentiment.

## Why Twitter?

Web scraping has always interested me in how much it can tell you about pop culture and human behavior in general. We put so much of ourselves in online spaces, so I wanted to see how online culture, specifically twitter culture, has changed as time has gone on. People often say that social media is a plague, but I have seen a lot of productive discussions to contrast against any percieved negativity as people realize the potential of being this globally connected. I wanted to test the hypothesis that social media has made us less coherrent or willing to start important diaologue. I also wanted to look at the sentiment behind the dialogue and compare it over approximately 8 years. For me personally, 2011 was around the time when I was first expressing myself on the internet, so it is interesting to see how nostalgia colors our view of the past.

## Data

The data for this project comes from a sample of the 2011 and 2019 [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) JSON files, where the top 1% of tweets were scraped from October of 2011 and September of 2019. Initially, I tried to use the entirety of the dataset which proved to be too much for my computer to process. The original data was about 2.2 GB for 2019 and 0.072 GB for 2011, and was broken up into various files that stored a couple thousand lines of JSON code. Of these files, I took 8 for each year which yielded about 13,000 tweets each.

However, these tweets were still in their rough form. My [initial run through](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/data_parsing.ipynb) showed that the unedited dataframes had about 161 columns. I decided to only keep the text, the user's language, and the date the tweet had been created. Then I pickled the data for later use. 

There was also a classifier built for the sentiment analysis portion of the analysis which used the open source data from [Sentiment140](http://help.sentiment140.com/for-students), a pre-existing algorithm for sentiment analysis. Both the classifier data and the data used in the project can be found [here](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/tree/master/data_samples)
