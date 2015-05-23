---
title       : Words
subtitle    : Show word frequencies for any website
author      : Qpias
job         : Data guy from Helsinki, Finland
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Words app
Insert URL in the textbox, select how many of the most common words you want to see listed, and click button.
* app: https://qpias.shinyapps.io/words
* code: https://github.com/qpias/words

## Motivation
I like to use R for text mining, especially to understand the content of documents. A simple text mining approach is "bag-of-words" where words are extracted disregarding form and order. Often you can figure out the topic of the document from the most common words.
<br/><br/>
http://en.wikipedia.org/wiki/Bag-of-words_model

---
## What
* The application uses the "tm" library to extract word counts from text documents.
* HTML tags are removed
* English stopwords (most common words) and common JavaScript words are removed
<br/><br/>
http://cran.r-project.org/web/packages/tm/index.html 

---
## Example

```r
library(tm)
library(xtable)
corpus = Corpus(VectorSource("hello ciao bye bye"))
fm = as.matrix(DocumentTermMatrix(corpus))
rownames(fm) = "frequencies"
print(xtable(fm), type = "html")
```

<!-- html table generated in R 3.1.2 by xtable 1.7-4 package -->
<!-- Sat May 23 18:15:42 2015 -->
<table border=1>
<tr> <th>  </th> <th> bye </th> <th> ciao </th> <th> hello </th>  </tr>
  <tr> <td align="right"> frequencies </td> <td align="right"> 2.00 </td> <td align="right"> 1.00 </td> <td align="right"> 1.00 </td> </tr>
   </table>

---
## Problems
* I originally stemmed the words, but the SnowballC library is not supported by shinyapps.io, and needs to be installed.
* Could not find an easy way  to remove all JavaScript
<br/><br/>
http://en.wikipedia.org/wiki/Stemming



