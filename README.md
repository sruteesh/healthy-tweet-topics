# Topic Modelling from Healthy Tweets

Extract Topics from Health related tweets

## Approach
* Classic case of Unsupervised Learning
    #### Input --> Embeddings --> Cluster (Topics) --> Top N Tweets (Topic Description) --> Keyword Extraction (Sub-Topics)

## Data
* Tweets from 16 different sources
* Around 63k tweets in english

## Preprocess
* Remove non-ascii characters
* Remove URLs
* Extract Hashtags
* Remove RT tags and owner information

## Identify Topics using Hashtags
* Since No information about the tweets is available, use hashtags to get rough idea on Topics of tweets

## Baseline
* Use the Standard LDA to extract topics 
* Used Gensim library

## Clustering (Kmeans + Universal Embeddings)
* Used sentence embeddings to encode the sentences
    * Used Universal Sentence Encoder to get sentence embeddings
* Used Kmeans Algorithm to Identify Tweet groups (topics)
* Find the closest sentence to the Cluster center (Gives Info about the Topic)
* Identify top n closest sentences to the Cluster center 
* Use these top n sentences to Extract Keywords 

## Textrank (Keyword Extraction)
Use Textrank to get weight each keyword from the group of sentences which were identified earlier (closest to the center)

## Learnings
* There are lot of irrelevant tweets which corrupt the Topic group (Discard them for further analysis)
    * Use distance from cluster center to discard irrelevant tweets
    * Also outlier tweets (which do not have many similar tweets based on cosine distance between the sentence embeddings) can be discarded
* Hashtags give good approximation about the topics of tweets

## Improvements
* Universal Embeddings were trained on generic texts, fine-tune them with domain specific texts and tweets like texts
* Use Other Embedding techniques (ElMo vectors, skip thoughts etc..)
* Extend Textrank to consider phrases (ngrams) as candidates

