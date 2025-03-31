---
title: "OCR'ing and analysing comic books - a workflow"
date: 2015-12-03
categories: 
  - "digital-humanities"
  - "history"
tags: 
  - "comic"
  - "donald-duck"
  - "ocr"
  - "spider-man"
  - "tesseract"
  - "voyant"
---

![spiderman](https://pimhuijnen.com/wp-content/uploads/2015/12/spiderman.jpg)I like experimenting with text analysis tools like Voyant. However, most tools for corpus linguistics don't account for historical change - which I am, as a historian, mostly interested in. Historians working with tools like these have to think of ways themselves to add a time scale to their analyses. The most straightforward way to do so is by arranging a corpus in a chronological order. Highly interesting, for example, is to study linguistic changes in successive volumes of newspapers or periodicals, as I do in my academic research.

Really just as an experiment, I've also tried analyzing volumes of comic books. I happen to possess some digital comic book archives, they have a nice chronological order, and they are quite under-studied as historical sources for changes in (popular) culture. As turning digital comic books (in cbr format) into analyzable text files took more effort than I realized, what follows is the workflow I constructed. I don't know whether it's the optimal way of doing so, but as someone who is new to bash commands, OCR'ing, and the combination of both, I had a lot of fun figuring this out. No, it's probably a long way from being optimal. More like quick-and-dirty, although it isn't quick either (depending on the volume of your dataset). But it does requires hardly any action, so for all its downsides it really is a fun way of experimenting with the (historical) text analysis of some original data.<!--more-->

The cbr format that digital comic books usually come in is really nothing more than a zip file of jpgs, made readable for digital comic book readers. The first thing I, therefore, did was changing the cbr extensions into normal zips line using the following command in the Mac terminal:

$ (for f in \*.cbr; do mv ./"$f" "${f%cbr}zip"; done)

Every single issue that's in my dataset now is an individual zip file. When extracted, they turn into folders that contain multiple jpgs. After unzipping, I delete all zip files, which are no longer needed. Next step is OCR'ing the jpgs. I do this with Tesseract OCR, which is open source and works well for image files (and is trained for various languages, including Dutch). More specifically, I use the VietOCR GUI, which I came across and has a fine usability, so does the trick for me quite easily. It has a 'bulk OCR' option that merely asks you to identify the source folders to start working.

Now, I wait. A single jpg is OCR'ed in matters of (tens of) seconds. However, a single comic book issue usually consists of twenty to thirty pages. And of the first series of The Amazing Spider-Man, to take one example I OCR'ed, 442 issues were published between 1963 and 1998. That makes 442 x 25 x 10 seconds = more than 1,800 minutes or 30 hours. In short, this is something I run over night and during weekends.

When OCR'ing is done, for every jpg I have a related txt file. The last step I have to do is merge all text files per issue into one large text file. This is something you can easily do by hand on the command line using the cat command, but you'll have to do each issue individually (assuming you would like to be able to separate each individual issue). To do this automatically, I use following bash script:

#!/bin/bash

for i in {1..442} do cat $i/\*.txt > \[specified folder\]/$i.txt done

This script presummes that the folders are numbered in a successive order (here, from 1 to 442). If not, they are easily renamed accordingly using Macs 'rename folders' option. This option will at once rename all selected folders. When issues represent a single year, you can, of course, also name the folders accordingly (so 1963 to 1998, for example). However, in the Spider-Man example I did not do this. This bash file just gave me 442 text files, numbered 1 to 442. For me, it was sufficient knowing how the issue numbers corresponded to the years of publishing, although I could have used to cat command a couple of times to merge all issues from a single year into text files-per-year.

Finally, I uploaded my dataset into Voyant tools, running my own Voyant server for extra memory. Unfortunately, here my story fizzles out a bit. I used the Spider-Man example here, because it was the only English speaking comic book series I tried thus far. Its OCR quality, however, is really bad. This is what Tesseract makes of the title page of issue 276 (the image above):

Ma.’ n’ CAN'T -nauez I'VE FINALLY ANAGED To LINMASK THE HOBGOBLI/V.’

Not much to make of that. OCR quality really depends on the way the text is written - the more the text resembles typescript, the better OCR will get. In this case, my idea was that quantity could make up for quality. Given that there is sufficient data, the OCR failures would perhaps become less significant. I don't know whether that worked, but I did play a little with Voyant's functionalities. Here, for instance, collocates of the words 'genetic', 'nuclear', and 'powerful':

\[gallery ids="1129,1128,1130" type="rectangular"\]

I started this post with making a point about implementing a time scale. Here's an example from the Dutch version of the Donald Duck comic books. Voyant lets you track the frequency of words (or strings of words) through the dataset at hand. When your data represents single years, which is the case here (the files represents the years from 1952 to 2014), the graph turns into a histogram. As a check for OCR quality I plotted the usage of the string 'donald duck' itself (together with the single words 'donald' and 'duck'), which should be present in every single issue.

![donald_duck](https://pimhuijnen.com/wp-content/uploads/2015/12/donald_duck.png)

Given the fact that every volume consists of about 52 issues (the comic was published once a week), the usage of 'donald duck' shouldn't fluctuate as it does according to this graph. OCR quality probably isn't great either. Apart from this, this final illustration shows that this type of analysis could - provided sufficient OCR quality - result in more than just searching for trends in the use of comic book figures. For example, these comic books were filled with advertisements. In this respect, comic books form terrific sources for studies into things like consumer culture. Here, a graph showing the trend of the word 'advertisement' in the Dutch Donald Duck:

![donald_advertisements](https://pimhuijnen.com/wp-content/uploads/2015/12/donald_advertisements.png)
