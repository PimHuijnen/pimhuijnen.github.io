---
title: "The Productivity Paradigm"
date: 2015-04-08
---

What would a distant reading analysis of early public debates on scientific management in the Netherlands look like? A logical start would be to consider the degree to which the concept of 'scientific management' was discussed in Dutch newspapers (i.e. in this particular corpus). However, bluntly querying "scientific management" would be an overly naive way to go about. Dutch newspapers would ordinarily have mentioned the concept in translation.

Then, however, the question rises: what translation? Several current Dutch equivalents of 'scientific management' circulated in the public sphere before WWII. 'Wetenschappelijke bedrijfsorganisatie' was as common as 'wetenschappelijke bedrijfsleiding' Less used was the term 'wetenschappelijke bedrijfsvoering', as was the original English expression.\[1\] Were there any other synonyms? Random checks of articles on the subject do not seem to suggest so. Nor does the list of all word variations of 'bedrijfs' within the corpus, generated with the use of regular expressions, point toward any other variants of the Dutch word for management.\[2\]

Also, references to Taylor--'Taylorisme', 'Taylor-stelsel', 'Taylor-systeem'--were being used as some kind of alternative for 'scientific management'. The specific context in which references to Taylor were used, and their possible distinction from more direct translations from 'scientific management' will be elaborated below. For a first glance, they are piled together to extract a subset of 'scientific management' within the KB-corpus.

This subset consists of 1175 documents in the KB-corpus in the period 1890-1939. Can we from a distant reading perspective say something about what these articles are about? A number of techniques are available to do so. A raw frequency based word cloud presents a visualization of the fifty most common (frequent) words used in all articles, in which 'scientific management' or 'taylorism' or equivalents are present as well. A stopword list prevents the cloud from being deluged with the most frequent (and, therefore, least revealing) words in Dutch language, like articles and conjugations of common verbs like 'be', 'go', 'make', or 'say'.

![Screen Shot 2015-04-02 at 12.17.34](https://pimhuijnen.com/wp-content/uploads/2015/04/screen-shot-2015-04-02-at-12-17-34.png)

Still, the words in the word cloud in themselves do not necessarily share any significant relation with the query words. From these kinds of word clouds one can only conclude that they are present in the corpus constituted by those query terms. However, the present terms do tell something about the inner coherence of this corpus. A relatively large number of words in the word cloud refer to the topic at hand. 'Taylor', for example, features prominently. Also noticeable are words indicating institutions and conferences ('instituut', 'organisatie', 'congres', 'voorzitter', 'vergadering', 'spreker'). The hallmark term 'efficiency' can also count among these words, given the existence of the Nederlandsch Instituut voor Efficiency (Netherlands Institute for Efficiency, founded in 1925) and the international conferences on scientific management that were regularly organized before 1940.

Other striking words in the word cloud are 'werk', 'arbeid', 'arbeider', 'arbeiders' ('work', 'worker', 'workers'), 'algemeen' and 'belang' (together meaning 'common good'), 'maatschappij' ('society'), 'staat' ('state'), 'minister' ('secretary'), and 'industrie' ('industry'). The term 'leven' ('to live') is another striking word in the cloud. Adverbs and adjectives are scarce among the most frequently used words, but those present are fairly positive: 'goed'/'goede' ('good' or 'well'), 'mogelijk' ('possible') and 'nieuw' ('new'). As a whole, this word cloud seems indicative for the overall content of the dataset. However, there are little surprising words in the cloud. As a result, the impression one gets from the word cloud is quite ubiquitous, and certainly not much differentiated.

A way to get a more discerned idea of the content (context) of a subset of documents like this is via topic modeling. This technique is based on a statistical probabilistic

\[1\] 'Wetenschappelijke bedrijfsleiding' yields 232 hits in the NL's newspaper corpus between 1890 and 1939, 'wetenschappelijke bedrijfsorganisatie' 215 hits, 'wetenschappelijke bedrijfsvoering' 45, and 'scientific management' 28 hits.

\[2\] This webtool allows for the use of regular expressions on a sample of 0.01 Percent of the NL's newspaper data. The command '\\bbedrijfs\\w\*\\b' yields all possible endings of the phrase 'bedrijfs' in this subset.
