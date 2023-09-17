Approach 1: Topic Modeling
Overview

*  Prepare the dataset by padding the comments and tokenizing the tokens.

* Using spaCy to eliminate commas and extract phrases with important teacher evaluation and difficulty-related words. With named entity recognition, quick access to word vectors, and extremely quick and accurate syntactic analysis, spaCy is a powerful tool to be use here.

* Building a neural network with Keras to determine whether a comment is connected to teacher evaluation or level of difficulty.

* Analyzing the model's performance using the test data set's correctness.

* We have also used the text-processing.com API which is a simple JSON over HTTP web service for text mining and natural language processing.

Analyzing

>We obtain accuracy of **71%** for star rating and **63%** for difficulty over the training data set.

>We used different dataset to test, over the test data set we get accuracy of **62%** for star rating and accuracy of **54%**  for difficulty

Topic modeling is useful when we try to get hidden patterns from text data, which can be beneficial in identifying important aspects of the text data.

The results is sensitive to the choice of hyperparameters, such as the number of topics to be extracted, which might hinder our accuracy.

*We consider tolerance of 1 in testing*






Appraoch 2: Sentiment Intensity Analysis, Version 1

Overview

A model for text sentiment analysis called VADER (Valence Aware Dictionary for Sentiment Reasoning) is sensitive to both the polarity (positive/negative) and intensity (strong) of emotion. It may be used right away on unlabeled text data and is included in the NLTK package.

Analyzing

Star Rating
>**Training data Mean Squared Error** : **1.16**

> **Test data Accuracy** : **63%**.

Difficulty Rating
>**Training data Mean Squared Error**: **1.48**

>**Test data Accuracy** : **65%**.

This model considers both polarity and intensity of emotions, which provides more nuanced results.

We haven't perform any hyperparameter tuning for this model

*We consider tolerance of 1 in testing*



Approach 3: Sentiment Intensity Analysis, Version 2

Overview**

In this version, we are doing test cleaning aggressively to evaluate if we get a better accuracy.
> We are removing punctuation and stopwords in addition to dropping NA fields.

> Code is similar to the last approach

> There is a significant in accuracy for Difficulty Rating and Star Rating accuracy also improved. We can see the impact of cleaning data. The loss increased, slightly.  

Analysis

Star Rating
> Traning MSE : 1.299601435661316

> Testing MSE : 1.2041118144989014

> Testing Accuracy : 65%

Difficulty Rating
> Traning MSE : 1.5125211477279663

> Testing MSE : 1.5

> Testing Accuracy : 73%



*We consider tolerance of 1 in testing*



Approach 4: Rescaling and word embedding


 Overview

In this approach, we are using Glove, the pre-trained word embedding.
We have also scaled the star and difficulty from 0 to 1. After that we gave this data to an RNN model.

Model architecture as follows,

Embedding layer - Dropout layer - 1-D convolution layer - 1-D Max Pooling - Bidirectional LSTM - Dense Layer

We have also used the text-processing.com API which is a simple JSON over HTTP web service for text mining and natural language processing.

 **Analysis**

 Star Rating
 > Testing Accuracy : 51%

 Difficulty Rating
 > Testing Accuracy : 51%


 *We consider tolerance of 1 in testing*
