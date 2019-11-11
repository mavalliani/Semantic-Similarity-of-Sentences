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


## Unsupervised Learning approaches:
For many practical scenarios, training data might not be available. Some unsupervised approaches can also be used to model for this problem.
Using K-means algorithm to group the questions in clusters and then classifying the similar/dissimilar based on that can also be employed. A simple approach to first determine the right number of clusters and then declaring similar has been shown here.
