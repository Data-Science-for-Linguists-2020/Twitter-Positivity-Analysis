# Diachronic Twitter Sentiment Analysis

## Natasha Kamtekar | nak142 | 4/24/2020

A link to the project guestbook can be found [here](https://github.com/Data-Science-for-Linguists-2020/Class-Plaza/blob/master/guestbooks/guestbook_natasha.md)

## Project Description
This project looks at Twitter data from the [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) from 2011 and 2019 respectively. It compares and contrasts tweeting habits from both points in time such as content, lexical complexity, tweet length, and tweet sentiment.

- How is popular content of either era percieved or talked about?
- Have tweets become a medium for displaying more complex sentiment than they used to be?
- How does this complexity relate to overall sentiment? 

## Project Data

The main data used in this project came from a sample of the 2011 and 2019 [internet archive](https://archive.org/search.php?query=twitterstream&sort=-publicdate) JSON files, where the top 1% of tweets were scraped from October of 2011 and September of 2019. There was also a classifier built for the sentiment analysis portion of the analysis which used the open source data from [Sentiment140](http://help.sentiment140.com/for-students), a pre-existing algorithm for sentiment analysis. The data used in the project can be found [here](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/tree/master/data_samples), the classifier data can be found on the Sentiment140 website linked above. 

## Table of Contents

- **Important documents**
	- [final_report](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/final_report.md)	
	- [LICENSE](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/LICENSE.md)
	- [presentation](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/Natasha%E2%80%99s%20Progress.pdf)
	- [progress_report](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/progress_report.md)
- **Folders**
	- [Data sample](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/data_samples)
		- 2011 dataset
		- 2019 dataset
	- [Notebooks](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks)
		- [build_classifier](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/build_classifier.ipynb): build the classifier for sentiment analysis. 
		- [data_parsing](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/data_parsing.ipynb): strips the tweet data to necessary columns
		- [data_analysis](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/data_analysis.ipynb) and [classifyanalysis](): different stages of the analysis process
		- [finalnb](https://github.com/Data-Science-for-Linguists-2020/Twitter-Positivity-Analysis/blob/master/notebooks/finalnb.ipynb): the final jupyter notebook
	-[Images]:
		- Contains images of all plots
