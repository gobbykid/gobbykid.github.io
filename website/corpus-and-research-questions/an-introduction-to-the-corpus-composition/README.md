---
description: Corpus composition, sources, balance, and sub-corpora.
---

# An introduction to the corpus composition

Talking about the corpus we have built, it is of great importance for us to stress on a concept of great importance that, under a specific perspective, may seem also as a disclaimer:

> all knowledge is situated. A less academic way to put this is that context matters. When approaching any new source of knowledge \[…] it’s essential to ask questions about the social, cultural, historical, institutional, and material conditions under which that knowledge was produced, as well as about the identities of the people who created it (D’Ignazio and Klein 2020, 152).

Therefore, this section aims not only at explaining how the corpus has been structured and why, but also at specifying the sources from which the texts have been chosen and downloaded, and the modifications made to them. This is crucial not only to let the reader know more about the adopted methodology, but also to let one reasoning about the “truth” that has been generated from the collected data.

Books have been extracted from Project Gutenberg ([https://www.gutenberg.org/](https://www.gutenberg.org/)) on the basis of the “Standardized Project Gutenberg Corpus”, an easy to download dataset with data concerning a frozen version of the Gutenberg Project's corpus ([Gerlach and Font-Clos 2018](broken-reference)). The dataset contains all the metadata of the texts held by Project Gutenberg and has been filtered according to particular parameters. Only texts that do not consist mainly of poems or nursery rhymes and that, according to the metadata, have children and/or juveniles as their primary audience have been kept. Moreover, only the ones whose authors are contained in the Wikipedia template named “[Victorian children’s literature](https://en.wikipedia.org/wiki/Template:Victorian\_children's\_literature)” under the label “authors” and in the list of children’s fiction authors on the “[Victorian Web](https://victorianweb.org/genre/childlit/index.html)” platform have been added to the final set of texts. If not already included in the previous extraction, also books coming from the Wikipedia “[List of 19th-century British children’s literature titles](https://en.wikipedia.org/wiki/List\_of\_19th-century\_British\_children's\_literature\_titles)” have been added to our corpus. Naturally, the last implicit requisite is that the books' publication date is included within the Victorian time period ([as previously defined by citing Encyclopedia Britannica](../../introduction-to-gobbykid-project/the-context-victorian-childrens-literature.md)).

All books are encoded in UTF-8 and the initial and final sections dedicated to Project Gutenberg's information have been deleted for processing purposes. Moreover, only the text of the fictional story contained into the book has been kept, while prefaces, and information related to editors and other publications have been deleted.&#x20;

The total number of downloaded books is 345, 160 of which have been written by men and 185 by women. However, among the chosen texts, men's ones are longer than women's. That is why the corpus has been processed in order to have a more balanced number of tokens to analyze.

{% embed url="https://github.com/gobbykid/corpus.git" %}
The GitHub repository containing the raw texts and the CSV file with the records of the books.
{% endembed %}

{% file src="../../.gitbook/assets/gobbykidCorpusPreBalancing.csv" %}
The CSV file containing the records of the books available in the corpus (pre-balancing).
{% endfile %}

