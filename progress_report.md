## Natasha Kamtekar

This is the `progress_report.md` for my project. 

Table of Contents:
- [Test Entry](#test-entry)
- [1st Progress Report](#1st-progress-report)

---

# Test Entry
## 2/6/2020
Created empty repo to hold all the files.

---

# 1st Progress Report
## 3/8/2020

### Current Progress
- Initially I tried to use tweepy to collect data based on hashtags, but that process only yielded a small number of results for a very niche topic. 
- Spent some time finding and analyzing datasets found online to see if it had relevant information (specifically dates). Eventually found [this site](https://archive.org/search.php?query=twitterstream&sort=-publicdate), which contained JSON files of twitter streams from 2011 to the present day. It is the "Spritzer" version of Twitter data, which is only 1% of tweets, but it seems like this site has multiple passes for data. 
- Created a [notebook](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/data_parsing.ipynb) file where I placed a sample of the entries into a dataframe in order to analyze further in the next phase. I am currently looking at pre-existing [open](https://github.com/nickdavidhaynes/spacy-cld) [source](https://polyglot.readthedocs.io/en/latest/Detection.html) [code](https://pypi.org/project/langdetect/) that might help me identify the language used in the tweet (since right now there is only data on the *user's* language). 
	- I want to start making classifiers to do sentiment analysis on the tweets I have found. 

### Sharing plan
- The data i've found is released under CC0, so there should be no issue sharing it in its JSON form. Any data i've edited and trimmed I might only share a sample of. Any code I create that might be useful to other people can be used only with credit. 

---

# 2nd Progress Report
## 3/22/2020

## Current Progress
- I have put both my data for 2011 and 2019 into a dataframe and cleaned it up so that it only displays the text, time, and language (which I have set to be english). To do this I used the langdetect library. I also created a tokenized list for both 2011 and 2019 in order to analyze frequency distrubution and bigrams.
- I have built a naive bayes classifier for my sentiment analysis. It could still use some work, so i'm going to continue tweaking that. I found an enormous corpus of already tagged tweets and was trying to manage the size of it. For my purposes I am only using part of it.

## License 
- I chose to go with GNU General Public License v3.0 because I wanted people to be able to use and modify my work and data, but ultimately give credit when they do. 
- The old data I pushed has the same license as I mentioned last time, but the data I used to build the classifier is also open to use as long as Sentiment140 is listed as the source. 

