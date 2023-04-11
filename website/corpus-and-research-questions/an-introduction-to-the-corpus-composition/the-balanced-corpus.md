# The balanced corpus

## Balancing the corpus

Given our research questions, we want our female and male corpora to be _large enough_, in order to allow meaningful results, while at the same time being _balanced_ according to certain criteria, in order for our dataset to be represenative of the whole population we are considering.

The balancing process is aimed at filtering the works in the original dataset in order to get two corpora satisfying the following criteria:

1. **Largest possible dimension**: we want our final corpora to include the largest number of texts from the original ones.
2. **Female vs male authors balance**: we want the corpus of female and male authors to be as equally sized as possibile, in terms of global number of tokens.
3. **Size-per-decade balance**: we want a balanced distribution of tokens amongst the decades within the considered timespan, inside both the female and male authors corpus.
4. **Authors-per-decade balance**: we want the variety of both female and male authors to be represented within each decade, i.e. we want to have, in each decade, at least one book by each author, if any work by such author is present for such decade inside the original corpus.

The balancing process starts from a fundamental observation: in our original corpus, which has been built to be maximally inclusive (therefore comprehending the maximum number of available texts for each author relevant to our research), the texts written by female authors are generally shorter in size than books written by male authors.

This is evident even in the bare count of global tokens for the female and male authors corpus:

* Female authors corpus:
  * Total number of words: 9458669
  * Number of books: 185
* Male authors corpus:
  * Total number of words: 14074486
  * Number of books: 161

Despite the larger number of books written by female writers, the female authors corpus is considerably smaller in size, in terms of number of tokens, compared to the male authors corpus.

{% embed url="https://plotly.com/~eliarizzetto/116/" %}

O

The way we approach our problem is by creating 3 new list of documents, one per (sub-)corpus, by **applying consecutive filters** on the original dataset. In applying such "filters", we must respect a **hierarchy of priority** that complies with the general goal, i.e. having the minimum difference in the number of tokens between male and female authors and between each temporal phase, while at the same time keeping the largest global amount of textual data and maintaining the variety of authors in each temporal phase.

In other words, we want to have the maximum amount of tokens for each decade, the maximum number of authors for each decade, **but** a similar number of tokens amongst the decades and, most of all, a globally similar number of tokens between the male and female writers. Given that some of these goals are conflicting (e.g., filtering out textual data to get the same amount of tokens for each decade conflicts with the principle of keeping the maximum amount of tokens globally), we first have to define an order of priority, i.e. identify the goals of the balancing process from the most important to the least important.

1. First, we want the data to be balanced (in terms of number of tokens) with respect to the author's sex.
2. Second, we want to keep the maximum number of authors present in the original corpus, as the presence of diverse authors conditions the variety of the dataset and its representativeness.
3. Third, we want to maintain the maximum global amount of tokens.
4. Fourth, we want the number of tokens to be distributed equally along the considered timespan, i.e. per each decade ther should be a similar number of tokens compared to the other decades.

#### **The `get_balanced_data` function**

We define a function `get_balanced_data()`, which takes in input one of the lists of dictionaries (male or female authors, or the whole dataset) and the number of books - defined by two different arguments associated with the author's sex - that we are willing to keep from each decade, for each author, according to the author's sex. The function returns a new list resulting from the filtering of the input list.

Since we know that books by female writers are shorter than the ones by males, we decide to keep from the "male" dataset the shortest books (i.e. the ones with a lower number of tokens), and from the "female" dataset the longest ones. We do so by sorting the dictionaries inside the input list by ascending value of the `tokens_in_book` key, and then taking the n _first_ elements (the shortest books) for _male_ authors, and the n _last_ elements (the largest books) for _female_ authors.

We want to apply this selection criterion consistently for each decade, and at the same time we want to keep in the final version all the authors present in each decade originally: the filter keeps at least one book by each author per each decade, regardless of the number of books to keep specified in input.

We might want to specify two _different_ values of the number of books to keep for male and female authors: in fact, in this way we can see which combination of values best satisfies the criteria we are considering. After several tries, we saw that keeping up to the _6_ _longest_ books by female writers and up to the _10_ _shortest_ books by male writers allows us to satisfy decently all the criteria: these values are set by default in the function definition.

### Balanced corpus statistics



|                                   | Total number of words | Number of books |
| --------------------------------- | --------------------- | --------------- |
| ♂️ BALANCED male authors corpus   | 8797218               | 109             |
| ♀️ BALANCED female authors corpus | 8534374               | 157             |
| ♀️♂️ Whole BALANCED corpus        | 17331592              | 266             |

{% embed url="https://plotly.com/~eliarizzetto/7/" %}

{% hint style="info" %}
See the [repository on GitHub](https://github.com/gobbykid/corpus\_balancing.git) and the Jupyter Notebook for exploring the code
{% endhint %}

## Lexical richness

In order to enter on tiptoe inside the project, a preliminary presentation of the differences through time and between the different corpora has been done with respect to the lexical richness of texts. This analysis has been performed in order to highlight a possible difference in the unique terms used by authors during the Victorian era.

The results of the analysis can be seen thanks to the following plot, where female authors texts lexical richness averages are presented along with the ones from male authors texts:

{% embed url="https://chart-studio.plotly.com/~Postitisnt/5" %}
Lexical richness plot
{% endembed %}
