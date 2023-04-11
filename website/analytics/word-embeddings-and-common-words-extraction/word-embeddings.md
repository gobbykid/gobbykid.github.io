---
description: Analogies and embedding space visualization
---

# Word embeddings

## Models and outputs

Thanks to w2v technique, we did different tries and decided, in the end, to adopt a model build on a large window size and that lays on the Skip Gram methodology to produce vectors. This choice derives from the will to provide a semantic-oriented perspective rather than a syntactical-oriented one.

The final output of this process aims at providing the possibility to visualize and reason on the semantic field of gender related words. In particular, we have produced two different visualizations of these vector spaces: one for the female authors corpus and the other one for the male authors corpus.

### A different kind of space exploration

In order to visualize the outputs of these analysis, you have to access the below links. Together with them, this is the [repository](https://github.com/Postitisnt/Embeddings-for-GOBBYKID.git) containing the configuration files, as well as the files with the vectorial representations of words.

{% embed url="https://projector.tensorflow.org/?config=https://raw.githubusercontent.com/Postitisnt/Embeddings-for-GOBBYKID/main/config/f_config.json" %}
Link to the embedding space projection of the Female authors corpus
{% endembed %}

{% embed url="https://projector.tensorflow.org/?config=https://raw.githubusercontent.com/Postitisnt/Embeddings-for-GOBBYKID/main/config/m_config.json" %}
Link to the embedding space projection of the Male authors corpus
{% endembed %}

We produced a brief video of how it is possible to explore the corpora:

{% embed url="https://youtu.be/RBhCD1gR8w0" %}
Exploration demo
{% endembed %}

### An interactive proposal

It is possible to use the embedding projector presented above to search for the words of the previous section (the ones related with the most common words used by female and male authors), in order to discover some particular and reiterated patterns that confirm many gender stereotypes.

The fact that the projector has been produced only for the entirety of the two corpora is not a problem, in fact, as you can read and see in the previous section, there are almost no differences between semantic fields in the years before and after 1880.
