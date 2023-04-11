# Word embeddings and common words extraction

The aim of this section is to extract, and dive into, the semantic connotations in which different genders are involved. Moreover, we will look for some kind of possible stereotype in gender related sentences.

## Workflow of the section

### Common words extraction

In order to display some statistics about the most common words used in gendered sentences, we computed a list of the most common words in female and male sentences that different gendered authors tend to use inside the texts that compose the related corpus.\
The easiest way to do that is to retrieve the previously created _word\_freq_ dictionaries and to take out from them the most common words from the '_female_' and '_male_' keys.\
From such list we extracted all the words used together with a specific gender classification.

After that, we decided to POS-tag the extracted words, in particular because we thought that for the analysis only nouns, adjectives and verbs were relevant.

#### Computing the relative frequency

Once the list of common POS-tagged words was ready, we computed the ratio of each one of the words for what concerns its relative presence in male and female gendered sentences.\
We took into consideration the possibility that a word may appear the same amount of time for both genders but, one possible situation is when it appears 10 times, for example, in 50 male sentences and 10 times in 200 female sentences. <mark style="color:red;">Basically, that is the reason behind the necessity to compute its</mark> <mark style="color:red;"></mark>_<mark style="color:red;">relative frequency</mark>_.

### Word embeddings

In order to display values representing words similarities, we first needed to create some models to train with respect to our corpora. Such models will be able to use _<mark style="color:red;">word embeddings</mark>_ in order to retrieve similarities between the words of each corpus. This has been accomplished thanks to the mapping of such words into feature-vectors.\
The aim of this section was to develop some different _word2vec_ models, each with different parameters.

At the end of the training session, we have decided which one was performing better in the definition of word similarities and saved such model (obviously, the models will be two, one for the female authors corpus and the other one for the male authors corpus).

#### Some background theory on word embeddings

The reason behind the need to develop more than one model for each corpus is that there are some different parameters (as well as hyperparameters) to adjust. These, influence the final output in a significant way.

Seen that, we have decided to use the _<mark style="color:red;">word2vec</mark>_ technique to produce the models.

#### Possible paths within word2vec

In the word2vec architecture, it is possible to use 2 different methodologies to retrieve/produce word embeddings:

* <mark style="color:red;">**CBOW**</mark> _<mark style="color:red;">(Continuous Bag Of Words)</mark>_ - this first methodology operates by trying to solve a sort of "fake problem": _given a context, the model tries to predict a target missing word_. This is the base on which the model is trained in CBOW;
* <mark style="color:red;">**Skip Grams**</mark> - this methodology operates in an opposite way, it tries to solve a similar problem but, this time, _the input is the target word and the output will be its context_.\


Together with these different ways to compute embeddings, we will try to change the _<mark style="color:red;">context-window size</mark>_ that is, basically, the amount of words that are part of the context we aim at analyzing (the size represents the amount of words on the left side and on the right side of the target word; e.g for a size of 3, the 3 words on the left and the 3 words on the right of a target word will be considered in order to extract feature values).\
The different window sizes are computed after reading the article [Dependency-Based Word Embeddings](https://levyomer.files.wordpress.com/2014/04/dependency-based-word-embeddings-acl-2014.pdf), which states that&#x20;

> _Larger windows tend to capture more topic/domain information, while smaller windows tend to capture more information about the word itself_.

To this end, we have produced three groups of models for each methodology, and these have been initialized with small window size, medium window size and large window size.

Finally, we decided to use a <mark style="color:red;">`vector_size`</mark>`=100` (it means we considered 100 features to describe the dimension of each word), this choice is based on the size of our corpora.
