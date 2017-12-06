# capstone
My final capstone project for DSI

## STREAMING/STORING TWITTER DATA AND REQUIRED INFRASTRUCTURE

Streaming:

- Create list of dialect specific keyword search terms to use for twitter streamers.
- Create Docker file containing tweepy authentication tokens + other modules added to the jupyter scipy docker image to make the code generalized enough to work with different instances.
- Stream prefiltered keywords list for each class (EG, and GULF). Requires a crone job in order to:
	- Collect 1-username, 2-tweet, 3-location.  
	- Decode Arabic Unicode characters.
	- Store data as jsonl or json on AWS instance. 
	- Automatically restart tweet streams in case of common errors. 
    
Storing:

- Store raw data into Mongo collection (e.g: `raw_gulf`, with documents being `raw_stream` and `raw_timelines`). 
- Raw data remains stored on AWS instance. 

Infrastructure: 

- Two t2.micros with unique oauth to stream two dialects to decrease chances of dialects mixing. 
- One t2.large for modeling and more computationally expensive tasks. 

## CLEANING THE DATA

Cleaning stages:
	- Using regex to filter out emojis, links, http, excluded Arabic unicode in many cases. An easier way to clean the data is to import tweet-preprocessor, a twitter preprocessing library.
	- Check for duplicates before converting document formats.
	- Pickle cleaned data into a seperate folder (e.g: gulf_twitter_pickled).     
- Store cleaned data into Mongo collection (e.g: `cleaned_gulf`, with documents being `cleaned_stream` and `cleaned_timelines`). 
    
## BASIC EDA AND VISUALIZATIONS
	- Inspect keyword documents for excessive advertisement and remove duplicates. 
	- Inspect geographic origins of keyword documents to determine the document's utility to the overall collection. 
	- Identify users who contribute most to the keyword stream and add them to the timelines stage
    
## ITERATIVE EDA, TOKENIZATION, AND SVD 

- Perform EDA, tokenization and SVD on collected data:
	- Check for term co-ocurrences in EG and Gulf documents and add to stopwords list. 
	- Subtract co-occurances of terms between dialects from the data before tokenization?
	- Identify dialectically different keywords and include in the twitter streaming pipeline.
	- Identify users with the richest dialectal tweets and add them to timeline streams. 
	- Confirm geographic origin of tweets and make term substitutions in stop word list as needed.
	- Continue rinsing and repeating until terms appear mostly in either one or the other documents.

## REPEAT PROCESS FOR TIMELINES REST API

## STORING IN MONGODB

- Storing should be taking place at each stage of the process. 
- Build up corpus, store in Mongo collection as two documents for each class, EG and Gulf.
- Store combined documents under a new collection on Mongo.

## EDA, TOKENIZATION AND SVD

- Use Stanford Arabic Parser (with built-in ATB) to further clean the data. Use Stanford Arabic Word Segmenter concurrently with Parser, before or after? 
- Use the three different techniques below and explore the best results:
	- Label encode, run Tfidf, SVD, latent semantic analysis
	- Label encode, run Okapi best match, SVD, latent semantic analysis
	- Label encode, run Kullback-Leibler Divergence Model, SVD. 
	- Perform EDA

## TRAIN/TEST ESTIMATORS ON COLLECTED DATA WITH ASSOCIATED CLASSES (EG & GULF) 

- Use clustering estimators: 
	- DBSCAN
	- KMeans
	- Spectral Clustering
- Use classifiers: 
	- Naive Bayes
	- Multinomial LR classifiers
	- Logistic Regression
- EDA:
	- Perform plotting, confusion matrix, classification report, roc curve, 

## DEEP LEARNING - TEXT CLASSIFICATION WITH RNN
- Word2Vec
- Word embeddings using Keras or Gensim

Note: The TF*IDF scheme is the best weighting scheme to be
used with the Arabic language when used separately
without stemming or stopwords removal. This
contradicts some previous research indicating that the
BM25 algorithm is better when used with Arabic [17].
One reason for this is that the term frequency portion
of the TF*IDF scheme in Lemur is calculated using the
term frequency portion in BM25 giving it the
advantages of both of schemes. A second is that in
Savoy and Rasolofo’s experiment the BM25 was
combined with a stemmer which particularly boosts the
results with Arabic language.


