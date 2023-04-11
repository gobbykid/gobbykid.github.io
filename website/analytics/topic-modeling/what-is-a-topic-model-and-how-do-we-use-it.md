---
description: A brief introduction to Topic Modelling
---

# What is a Topic Model and how do we use it?

#### Topic model: definition

A Topic Model is a type of probabilistic model for automatically extracting the topics hidden in a set of documents, where a topic is an inferred cluster of words that have been found, by an algorithm, to be likely to constitute a semantically coherent "theme".

The assumption behind this is that each document in the dataset is the result of a combination of possible topics, and that words that more often co-occur accross the corpus are more likely to be semantically linked between them and represent one of these topics. In other words, the model identifies words that tend to co-occur together in multiple places in multiple documents within the dataset.

The whole clustering process is performed by the model in an unsupervised way, the number of topics being the only parameter set externally by a human. This means that the machine does not rely on any a-priori definition of what is a topic, nor on semantic notion of any kind: the only, internal, criteria to group the words are related to words' frequency in multiple contexts inside the corpus.

As mentioned in the documentation of [MALLET,](https://mimno.github.io/Mallet/topics.html) the software at the core of the process we will adopt in topic modeling the Gobbykid corpus, "topic models provide a simple way to analyze large volumes of unlabeled text. A "topic" consists of a cluster of words that frequently occur together. Using contextual clues, topic models can connect words with similar meanings and _distinguish between uses of words with multiple meanings_”.

#### The importance of topic models

This is in fact a key point: when it comes to word sense disambiguation, other text-mining techinques like [KWIC lists](https://en.wikipedia.org/wiki/Key\_Word\_in\_Context) and [collocates](https://en.wikipedia.org/wiki/Collocation\_extraction) require thorough human interpretation to determine the meaning of each indexed word, whereas topic modelling takes care of this automatically, "inferring information about individual word senses based on their repeated appearance in similar contextual situations" (Jockers 2013, 124). By treating the documents as [bag of words](https://en.wikipedia.org/wiki/Bag-of-words\_model), the model is able to make its inferences starting from a much wider context than, for example, collocates lists and without regard to the position of the contextual elements (the whole document being the "bag" in which the word is contained).&#x20;

#### The goal of our topic model

We want to topic model our corpus primarily to see what are the themes female and male authors write about in their books. In order to do so, we need each extracted topic to be as coherent as possible, i.e. the words contained in each topic must be semantically close enough to allow a human to easily interpret the general semantic area represented in each topic, basing his/her decision on the knowledge of the documents in the corpus. (Jockers 2013, 125).

### Research questions

1. What are the dominant themes in the books written by female and male authors?
2. How does the probability of meaningful topics (i.e. how much a theme is represented) vary in time accross the corpus? Is it possible to identify any correlation between the likelyhood of certain topics to be present in a book, and its publication year and its author's sex?



&#x20;



