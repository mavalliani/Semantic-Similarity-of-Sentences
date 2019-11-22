# Semantic Similarity of Sentences
Finding semantic similarity has been a work in development in the domain of Natural Language Processing. The range of applications range from search to text summarization to conversational AI. But there has not been a clear winner-model on all the aforementioned domains. The purpose of this text is to summarize the methods used for the problem at hand and build an intuition for model selection for the reader. 
The differentiating factor:
The semantic similarity between 2 words can easily be established using word embedding. Similarly large pieces of text are relatively easy to work with as the offer a lot of room for meaningful feature engineering. So for this essay, we are focusing on sentences. Pairs of sentences, assumedly written by different authors, are particularly hard as they:
1.	Assume prior knowledge of the audience.
2.	Very small number of words to work with.
3.	Feature set of one sentence pair does not translate to the feature set of the other pair. [this can be thought of as a trap for newbees who might vectorize the data and model it]
4.	Spelling mistakes can be found. [We ignore this problem, although we consider broken sentence structure].

### Dataset and Code:
The base dataset we shall be using will be “Quora Question Pair” challenge of Kaggle, which some may attribute, falls under the broader category of search. The training data has been hand-labelled, so assumed to be true.
The code of this essay has been hosted here.

## Methods to Model:
### Common-word Feature Model:
This method is the simplest to think of and has its origins in the “set theory”.  After lemmatization, we use the ratio of the intersection-count with the union-count. Higher the ratio, the similar the sentence is. 
This method has proven to be bad with short text data.

### Cosine Similarity with Word-Embeddings:
Vectorizing the sentence in an N-dimensional space, cosine similarity gives us a (-1,1) measure of the similarity which directly derives from the inner product of the vectors.
For sample code, I have used Glove embedding. Average of the word embedding of the sentence have been used. Our performance increased from the common-word model but still lagging way behind from a “release worthy” point. This model can be used as a baseline model.
***Smooth Inverse Frequency*** method also falls under this method where instead of assigning flat and equal weights to all words, we assign weights proportional to the inverse of the frequency in the corpus. This weight is also controlled by a learning rate.

### Word Mover’s Distance:
This method comes from Matt Kusner and team from Washington University, where the introduce a concept of ‘travel’. Quoting the authors, ‘The WMD distance measures the dissimilarity between two text documents as the minimum amount of distance that the embedded words of one document need to “travel” to reach the embedded words of another document’. 
So the more the words have to travel, the more the distance and the more dissimilar the documents are.

### Sentence Encoding Methods:
Just as words have been transformed into word embedding, there have been attempts to encode sentences into embedding vectors. Using sentence embeddings for other NLP tasks can be attributed as a form of Transfer Learning. More importantly, Sentence encoding, unlike Word Embedding, is obtained through supervised training. This can help extract meaningful results for our problem. It also accounts for word order in the sentences (eg. Dog bites the man; Man bites the dog) making it more meaningful.
We use 2 different sentence embeddings:
1.	Infersent – by facebook
2.	Google Sentence Encoding – by Google
Google Sentence Encoding outperform Infersent for out given task.


## Unsupervised Learning approaches:
For many practical scenarios, training data might not be available. Some unsupervised approaches can also be used to model for this problem.
Using K-means algorithm to group the questions in clusters and then classifying the similar/dissimilar based on that can also be employed. A simple approach to first determine the right number of clusters and then declaring similar has been shown here.
