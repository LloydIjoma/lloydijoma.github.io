---
layout: post
title:  "simple-step-by-step-guide-to-text-mining!"
date: 2018-05-15
tags: [Text Mining]
header:
   image: "/images/projects/download.jpg"

except: "Text Mining"
---

 Text mining provides a collection of techniques that allow us to derive actionable insights from data. 
 It is estimated that over 70% of potentially use-able business information is unstructured, often in the form of text data.
 In this article, we will explore the very simple step by step guide to text mining using R.
 
 
 First, you’ll need to ensure you have the most recent version of R, head over to http://cran.r-project.org/ to download it.
You can copy and paste the following commands into the R Console, although, we use R-Studio and would recommend it.

Then you’ll need to install “tm”, the text mining library for R.
Once it’s installed you need to load the TM library into your session.
#Load Library TM
library(tm)
Use setwd() to change the working directory to wherever you saved your CSV file to (note that you need to use a double forward slash in windows).
#set working directory
setwd(" ")
Then Read the file into your R session
# read File
reviews <- read.csv ("reviews.csv", stringsAsFactors=FALSE)
You can then View the content of the file
# view document 
str(reviews)
Now we start using the tm package.The tm package is designed for comparing different texts against each other. These are the steps the tm package expects you to take:
#combine all data together

review_text <- paste(reviews$text, collapse=" ")
Set up a source for your text and Create a corpus from that source (a corpus is just another name for a collection of texts)
#set up corpus

review_source <- VectorSource(review_text)
Corpus <- Corpus(review_source)
Next, we begin cleaning the text. We use the multipurpose tm_map function inside tm to do a variety of cleaning tasks:
#Start Cleaning the data

Corpus <- tm_map(Corpus, content_transformer(tolower))
Corpus <- tm_map(Corpus, removePunctuation)
Corpus <- tm_map(Corpus, stripWhitespace)
corpus <- tm_map(Corpus, removeWords, stopwords("english"))

# view Stopwords
stopwords("english")
Depending out what you are trying to achieve with your analysis, you may want to do the data cleaning step differently. 
 Create a document-term matrix, which tells you how frequently each term appears in each document in your corpus
#making a document term matrix
dtm <- DocumentTermMatrix(corpus)
dtm2 <- as.matrix(dtm)
We then take the column sums of this matrix, which will give us a named vector.
#finding the most frquent terms
frequency <- colSums(dtm2)
frequency <- sort(frequency, decreasing = TRUE)
And now we can sort this vector to see the most frequently used words:
#Sort Frequency
head(frequency)
We plot a word cloud
#Load Library wordcloud
library(wordcloud)
words <- names(frequency)
Let’s plot the top 100 words in our cloud.
wordcloud(words[1:100] , frequency[1:100])
This is far from the prettiest word cloud you’ve ever seen. And I hope it inspires you to try a piece of text analysis.