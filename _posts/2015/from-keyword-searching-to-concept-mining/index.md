---
title: "From keyword searching to concept mining"
date: 2015-12-03
categories: 
  - "digital-humanities"
tags: 
  - "dictionaries"
  - "gensim"
  - "keywords"
  - "koninklijke-bibliotheek"
  - "mallet"
  - "tf-idf"
  - "topic-modeling"
---

![keyword10](https://pimhuijnen.com/wp-content/uploads/2015/12/keyword10.png)Historical newspapers have traditionally been popular sources to study public mentalities and collective cultures within historical scholarship. At the same time, they have been known as notoriously time-consuming and complex to analyze. The recent digitization of newspapers and the use of computers to gain access to the growing mass of digital corpora of historical news media are altering the historian’s heuristic process in fundamental ways.

The large digitization project the Dutch National Library currently runs can illustrate this. Until now, the KB has made publicly available over 80 million historical newspaper articles from the last four centuries. Researchers (as well as the wider public) are able to do full-text searches in the entire repository of articles through the KB’s own online search interface Delpher . Instead of manually skimming through a selected numbers of editions or volumes this functionality allows for the searching of particular (strings of) keywords within the entire corpus. As basic as it may seem, full-text searching completely overturns the way in which historians are used to approach newspapers. Instead of the successive top-down selections historians traditionally made in order to gradually isolate potentially interesting material, keyword searching treats the corpus as a singular bag of words and, therefore, enables researchers to immediately dive into the texts that meet their search criteria.<!--more-->

At the same time, keyword searching has some serious shortcomings for the use in (cultural) historical research. Historians commonly work with texts, but are rarely interested in language per se. Rather, they use written or spoken sources (be it correspondence, literature, diaries, or news media) to gain access to past cultures, ideas, or mentalities. The things that historians are mostly interested in, are often not made explicit (e.g. the Enlightenment attitude, generational conflicts) and difficult to abstract into singular keywords (modernity, secularization). Doing historical research with keyword searching is like painting a canvas using felt-tip pens: it loses every inch of subtlety.

This piece of code, a program named 'Keyword Generator' (KG) represents a technique of dictionary extraction to address this problem. Juliette Lonij of the KB developed it in the context of my researcher-in-residence fellowship at the KB's research department. The use of dictionaries is able to bring greater subtlety and diversity into digital historical scholarship. The more elaborate these dictionaries are, the more they overcome the contingency that comes with the use of singular keywords in search strategies. Several research projects that have incorporated the use of highly domain- and time-specific word-lists ('dictionaries'), have already shown this. Text classification algorithms, for example, have helped find the most obvious indicator words for articles about strikes in the Dutch newspaper corpus. Implicit dictionaries based upon the Mallet package's topic modeling functionality has assisted in finding Darwinian motives in Danish literature. Topic modeling was also used in building a neoliberalism dictionary to study Colin Crouch's post-democracy thesis in German historical newspapers.

From the wide variety of techniques scholars have developed to build and use dictionaries, this project found most inspiration in the topic modeling-based method of the ePol Projekt. However, rather than aiming at building an optimal infrastructure for dictionary extraction of our own, based on existing techniques, our project centered around practical usability. We sought to develop a (set of) tool(s) for working with dictionaries tailored to the computational expertise to be expected from, but also the specific needs of professional historians (and humanities scholars in general). One of the aims of the KB's Researcher-in-residence program, in addition, is that resulting (open source) tools and techniques are usable by the wider public searching the National Library's databases of historical newspapers, periodicals, and books.

#### **Installing**

The Keyword Generator program can be found here on Github. To use KG, Python should be installed (KG is developed in Python). Gensim should be installed as well. To use the functionalities of KG to the full, also Mallet should be installed.

KG itself does not require installation, only unpacking of the zip file. Unzipping 'Keyword generator.zip' results in the creation of a folder 'Keyword generator', in which four files (corpus.py, corpus. pyc, keywords\_lda.py, keywords\_tfidf.py) and one subfolder 'Data' appear. The 'Data' subfolder in turn contains three subfolders of its own: 'documents', 'models', and 'stop\_words'. It is up to the user to put his own stop word lists in the last of these folders, dependent on whether or not he wants to leave stop words out of the equation. In general, KG is not language specific. Obviously, the use of stop words is. Lastly, in the 'documents' folder the (collections of) texts are to be put from which KG will derive a word list. The input should consist of one or more text files (.txt, UTF-8).

KG works from the command prompt. All commands are to be given from within the 'Keyword generator' folder. For more information on how to navigate on the command line, see, for example this tutorial (Mac) or this one (Windows).

#### Different methods of generating word lists

To convincingly use word lists as representations of ideas in humanities scholarship presupposes that one is able to argue (to a certain degree) for the appropriateness of the list he or she works with. This means, on the one hand, that transparency and user flexibility have received prominence in the development of KG. On the other hand, agility has been prioritized over the deployment of exhaustive computational means. In other words: there are more elaborated methods to extract word lists from collections of documents, but those require greater computational skills, computer power and/or time, and are, thus, more difficult to use in an explorative fashion. At the same time, meeting the demands of tool criticism was crucial in every step in the development of KG. Therefore, the risk of blackboxing was avoided wherever possible, while at the same time granting the user-expert as much control as possible.

These considerations have resulted in three separate methods for generating dictionaries that are implemented in KG:

1. TF-IDF
2. Gensim LDA
3. Mallet LDA

All methods have in common that they highlight (statistically) 'notable' words, derived both from the frequency of particular words in the document collection and the particularity of those words. The main difference between the first, and the second/third method of generating word lists is the use of topic modeling in the latter.

The first method will highlight words that have come to the fore based on tf-idf ("a numerical statistic that is intended to reflect how important a word is to a document in a collection or corpus"\*). In other words, when working with more than one document, the word list will consist of words that are most particular for each of the individual documents in comparison to the rest. The user can also split his document(s) into variable parts (see below) that then form the backbone of the tf-idf equation.

When using either the second or the third method, generating word lists becomes a two-step procedure. First, first topic models - statistical models that combine words appearing together above average to jointly represent the 'topics' that occur in a set of documents\* - are made from the (collection of) text(s). Second, the final word lists are based on the words present in the topics, while scoring is based on the frequency of appearances in the topics. Consequently, when choosing between either of the three methods, the user first has to ask himself whether he thinks topics (or: the interrelation of words within the documents used) are relevant for building dictionaries.

KG offers two separate ways of computing topic models (Gensim and Mallet) to avoid dependency on either one. The user can flexibly choose between them or run the algorithm multiple times and compare the results of both topic modeling methods.

##### Method 1: TF-IDF

The most straightforward command to use the tf-idf algorithm is 'python keywords\_tfidf.py'. Two settings can be changed:

- First, the number of keywords that the model should result in (default = 10) can be altered using the -k command. So, -k 100 results in a word list of 100 words, -k 50 in one of 50 words, etc.
- Second (particularly relevant when working with a single txt-file), the -d command collections the number of words in that determines the partitioning of the document(s) used. -d 1000, for example, splits the document(s) in parts of 1000 words. These parts (and not the separate documents that might be used) are then used to compute the tf-idf score.

\[gallery ids="1243,1197" type="rectangular"\]

##### Method 2: Gensim LDA

The simplest command to generate word lists based on Gensim's topic modeling procedure is 'python keywords\_lda.py'. Several settings can be tweaked:

- \-t sets the number of topics that will be modeled. Default is 10, but this can be changed to any (reasonable) number. -t 100, for example, will result in 100 topics
- The number of words can be altered with -w. Default, again, is 10. -w 25 will yield 25 words per topic
- The number of keywords that the model should result in (default = 10) can be altered using the -k command
- The partitioning of the document(s) can be modified using the -d command, followed by number of words the parts should consist of An example of the Gensim command could, therefore, look like 'python keywords\_lda.py -t 50 -w 25 -k 100 -d 1000'.

 

##### Method 3: Mallet LDA

KG will by default use Gensim's topic modeling. To use Mallet's method of topic modeling instead, the -m command is needed. After that, KG requires the full path to Mallet's executable file on the computer. A KG command using Mallet could (on my computer), for example, be like 'python keywords\_lda.py -t 100 -w 20 -k 200 -d 1000 -m /Users/huijn001/tools/mallet-2.0.7/bin/mallet'

 

![mallet](https://pimhuijnen.com/wp-content/uploads/2015/12/mallet.png)

##### Excluding topics

When using topic models to generate word lists, the user is given the opportunity to go through the topics before the actual word list is generated. This gives the user the chance to exclude topics that are relevant to the topic of interest. After the topics are modeled, the program will stop and ask for topics to be excluded. The user can give the numbers of the topics (comma-separated) that should be ignored. A simple \[enter\] will include all topics in the step of generating the word list.

![keyword](https://pimhuijnen.com/wp-content/uploads/2015/12/keyword.png)

#### Evaluation

An evaluation in terms of generic precision and recall for any of the variables would have been counter-intuitive. After all, there is no one best way to computationally derive word lists from any given text or collection of texts. Instead, the dictionary extraction methods have been evaluated and improved by comparing automatically generated dictionaries with ones that were built manually, based on domain knowledge. Comparing the results of query searches based on different dictionaries in the KB’s digitized newspaper archive was used as an additional evaluation method: dictionaries could be compared in terms of the ranking of some key articles about a particular topic, since the archive's Solr search engine scores the results of an OR-query (the search string, in which we expressed the dictionaries) on the basis of the number of times query words appear in an article, among other things.

\[gallery ids="1198,1196" type="rectangular"\]

The case study that was used to test, evaluate, and apply the tools and techniques under development was the impact of American scientific management ideas in the Dutch public media before WWII. The 'managerial revolution' is one of the more eye-catching ways in which Dutch language and culture appropriated American ideas. The word 'management' itself, but also concepts like 'efficiency', 'consultancy', or 'accountancy' are now generally understood as Dutch. Even so, it were American ideas that influenced the family businesses that dominated Dutch economy around 1900 into rationalizing and professionalizing. Equally, the first Dutch firms for organizational advice were inspired by scientific management theories from across the Atlantic - although it took a while before they started calling themselves 'consultants'.

The professionalization of Dutch business is a well-studied field of history. The existing literature proofs beyond questioning that it were American ideas that stood at the base of this development. However, to what extent the American nature of scientific management theories trickled down into the public sphere is less well known. This is a relevant question, considering the dominant narrative of America as an inspiration for European culture and economy during the 20th Century. Looking at ways in which scientific management ideas were related to America in the Dutch public sphere, can provide more depth and differentiation to the idea of the Americanization of the Netherlands in this period.

To do this, the use of dictionaries for search queries is a valuable asset. After all, it would hardly convincing to restrict oneself to search for the term 'Taylorisme' - after the most prominent American managerial thinker known in the Netherlands at the start of the century Frederick W. Taylor. Apart from the question which of the translations for Taylorism - 'taylorisme', 'taylorstelsel', 'taylorsysteem', etc. - would be most appropriate, the term does in no way fully grasp the debate revolving around scientific management in the Netherlands. The same goes for the concept 'scientific management' itself, which was concurrently translated as 'wetenschappelijke bedrijfsleiding', 'wetenschappelijke bedrijfsvoering', and 'wetenschappelijke bedrijfsorganisatie'.

The idea of dictionary searching is that it represents a way to study the impact of historical theories, concepts, and ideas without being restricted to search (in digital datasets) for the names of these theories or ideas. The graph below compares documents in the KB corpus containing words starting with 'taylor' (which leads to false positives, for it includes the name 'Taylor' itself, which, obviously, does not necessarily have to refer to Frederick W. Taylor) with documents containing at least ten of the given query words, derived from Taylorism literature. This could be a much more differentiated way to look for Taylorism in the Dutch newspapers.

![keyword7](https://pimhuijnen.com/wp-content/uploads/2015/12/keyword7.png)

Another way to put dictionaries into practice is to compare the most striking words from different - or competitive - theories to focus on the contrasts in word use between those theories. Focusing, in this case, on the differences between Taylor on the one hand, and Dutch theorists of scientific management on the other could give insights into what in this idea was regarded as typically American and what as Dutch. Words referring to hierarchy and control of workers ("beheer", "leiding") derived from Taylor's De beginselen der wetenschappelijke bedrijfsleiding (1913, the Dutch translation of his Principles of Scientific Management of 1911) might be indicators for a notable difference with the works of Ernst Hijmans and Jac. van Ginneken. This difference underlines the idea that Dutch thinkers focused less on the subordinate position of workers than Taylor did.

![keyword8](https://pimhuijnen.com/wp-content/uploads/2015/12/keyword8.png)

#### Step 2: Visualizing dictionaries

The KB has developed a simple tool to use the words from the word list to search the KB newspaper archive and to visualize the appearance of the words in the corpus over time. The so-called Dictionary can be found on www.kbresearch.nl/dictionary. The tool enables one to visualize documents in the corpus over time that contain a given number of words from the word lists (the query words), although it won't tell you which words. By clicking on a point in the graph, a webpage with DOI-links to all results from that particular year is provided.

The user has the opportunity to switch between relative and absolute results. Also, the timelines from multiple queries can be shown in one graph. The tool lists the queries, the number of results and the minimum number of words from the query that all results should contain. Visualizing the search results from different dictionaries can be considered as representing shifting discourses in historical news media. Plotting the number of articles containing a user-specified number of words from any given dictionary can present trends in discourse-specific vocabulary usage over time.

Whereas existing historiography, for example, suggests a continuing use of scientific management vocabulary in the Netherlands since its introduction in the 1910s, our project presents a more differentiated picture. Dictionary searches in the KB's newspaper corpus show how the use of words in public media connected to the sphere of scientific management (based on context-specific literature) waned after the WWII and how they made room for a new vocabulary belonging to a new era.

As a more general conclusion, this case study shows that (combinations of) ordinary words (in this instance, for example, 'time', 'work', or 'supervision') might be more distinguishing to trace discursive discontinuities than the 'big' words (like 'taylorism' or 'neoliberalism') that historians traditionally have focused on.

![keyword9](https://pimhuijnen.com/wp-content/uploads/2015/12/keyword9.jpg)
