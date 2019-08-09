---
layout: single	
title: "19 Books Every Aspiring (Or Experienced) Data Scientist Should Read"
permalink: /learn-data-science-reading-list/
author_profile: false

---

---
<meta property="og:image" content="/images/fulls/book-pen.jpg">
<meta property="og:image:type" content="image/png">
<meta property="og:image:width" content="200">
<meta property="og:image:height" content="200">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@jmzledoux">
<meta name="twitter:creator" content="@jmzledoux">
<meta name="twitter:title" content="19 Books Every Aspiring (Or Experienced) Data Scientist Should Read">
<meta name="twitter:image" content="http://jamesrledoux.com/images/fulls/book-pen.jpg">


{% include base_path %}

Whether you're an aspiring data scientist or a seasoned professional, these are 19 books that will help you improve your skills in machine learning, data analysis, visualization, statistics, and more. I've read and can highly recommend them all.

I've split this data science reading list into a few categories, but some may naturally belong in several groups (R for Data Science, for example, is great for learning both data visualization and analysis.) And just so you know, I may collect a commission from Amazon for any books you purchase using these links.

# Machine Learning (Theoretical)

### 1. [Introduction to Statistical Learning — James, Tibshirani, and Hastie](https://www.amazon.com/gp/product/1461471370/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1461471370&linkCode=as2&tag=ledoux-20&linkId=8c1a9dfaf14a4c03008255088c16035e){:target="_blank"} - $21.72

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=1461471370&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/1461471370/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1461471370&linkCode=as2&tag=ledoux-20&linkId=ea6977a721ab1aa4a633767d99273c35){:target="_blank"} A good first book on machine learning. Shows how most popular machine learning algorithms work, and also teaches a proper workflow for training and evaluating models (e.g. train/test splits, cross validtion, picking a loss function.) Allows a reader to get an intuitive grasp of what is going on inside the “black box”, but is a little too far on qualitative side if one hopes to gain a full understanding. For a deeper dive, see the advanced version Elements of Statistical Learning. 


### 2. [Elements of Statistical Learning — James, Tibshirani, and Hastie](https://www.amazon.com/gp/product/0387848576/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0387848576&linkCode=as2&tag=ledoux-20&linkId=509f4ea283d40c10e84100e24652b3e6){:target="_blank"} [*HIGHLY RECOMMEND*] - $30.60

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0387848576&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0387848576/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0387848576&linkCode=as2&tag=ledoux-20&linkId=509f4ea283d40c10e84100e24652b3e6){:target="_blank"} Similar to Introduction to Statistical Learning, but much more mathematically dense. This is my favorite reference book for machine learning theory. Topics include generalized linear models, additive models, bagging, boosting, tree-fitting algorithms, random forests, gradient boosting, and much more. It's worth reading several times.

### 3. [Learning from Data -- Abu-Mostafa and Magdon-Ismail](https://www.amazon.com/gp/product/B0759M2D9H/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B0759M2D9H&linkCode=as2&tag=ledoux-20&linkId=acbecd130e1361fed68a6e73913fa2e4){:target="_blank"} - $45.00

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=B0759M2D9H&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/B0759M2D9H/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B0759M2D9H&linkCode=as2&tag=ledoux-20&linkId=acbecd130e1361fed68a6e73913fa2e4){:target="_blank"} Another machine learning book that focuses on theory. It won't show you how to train your own models, but it will help to understand why models work and what guarantees we're able to make about learning and generalization. Less focused on specific ML algorithms, and more focused on the properties of learning and generalization.

### 4. [Deep Learning -- Goodfellow, Bengio and Courville](https://www.amazon.com/gp/product/0262035618/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0262035618&linkCode=as2&tag=ledoux-20&linkId=2337da010dc9fac2bcbf02d5f196e533){:target="_blank"} [*HIGHLY RECOMMEND*] - $25.01

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0262035618&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0262035618/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0262035618&linkCode=as2&tag=ledoux-20&linkId=2337da010dc9fac2bcbf02d5f196e533" ){:target="_blank"}  A balance of intuition, applicability, and theory that this field has been lacking. Begins with the nuts and bolts of feedforward networks, and then goes into depth about the state of the art in model regularization, optimization, and various model classes and architectures. Filled with useful tips and tricks for implementing models. This is the best book out there right now for learning how deep learning works.

# Machine Learning (Practical / Applied)

### 5. [Deep Learning with Python -- Francois Chollet](https://www.amazon.com/gp/product/1617294438/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1617294438&linkCode=as2&tag=ledoux-20&linkId=7e01295bf925a5f08fb1de8c1b3a7522){:target="_blank"} - $24.48

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=1617294438&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/1617294438/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1617294438&linkCode=as2&tag=ledoux-20&linkId=7e01295bf925a5f08fb1de8c1b3a7522){:target="_blank"}  A handy reference for Keras. This book is helpful for bridging the gap between beginner deep learning tutorials and more advanced / state-of-the-art methods. It's not the best for learning theory, but will help you to implement what you read in papers.


# Working with Data  (Python an R Programming)

### 6. [R for Data Science -- Wickham and Grolemund](https://www.amazon.com/gp/product/1491910399/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491910399&linkCode=as2&tag=ledoux-20&linkId=6ff0d6061908a54acb2b7098b98bfe3b){:target="_blank"} [*HIGHLY RECOMMEND*] - $18.17

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=1491910399&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/1491910399/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491910399&linkCode=as2&tag=ledoux-20&linkId=6ff0d6061908a54acb2b7098b98bfe3b){:target="_blank"}  An absurdly useful book for learning how to manipulate data with R and the Tidyverse (dplyr, ggplot, forcats, etc.) I read this once when I was first learning R and again after a few years of experience and learned new things each time. This book will make anyone better at data analysis, visualization, manipulation, and cleaning.


### 7. [Advanced R -- Hadley Wickham](https://www.amazon.com/gp/product/0815384572/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0815384572&linkCode=as2&tag=ledoux-20&linkId=69e02c35135b435b40a6fdd98a5a525e){:target="_blank"} - $53.73

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0815384572&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0815384572/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0815384572&linkCode=as2&tag=ledoux-20&linkId=69e02c35135b435b40a6fdd98a5a525e){:target="_blank"}  This book will teach you how the R language works on a much lower, more technical level. It's a useful book for helping advanced users write more performant code. It's also useful for people learning R whose background is primarily in other languages, as it will help to draw parallels between R and other languages. 


### 8. [Analyzing Baseball Data with R -- Albert and Marchi](https://www.amazon.com/gp/product/0815353510/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0815353510&linkCode=as2&tag=ledoux-20&linkId=5f4fd2083b034550b17c37ed7fab29b5){:target="_blank"} - $49.66

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0815353510&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0815353510/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0815353510&linkCode=as2&tag=ledoux-20&linkId=5f4fd2083b034550b17c37ed7fab29b5){:target="_blank"}  This book focuses on baseball data specifically, but is filled with data analysis and visualistion examples in R. It's filled with real-world examples of munging data to answer questions and understand rich data sets (in this case, baseball data).

<br>

### 9. [Python for Data Analysis -- Wes McKinney](https://www.amazon.com/gp/product/1491957662/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491957662&linkCode=as2&tag=ledoux-20&linkId=eff92247940c967299befaed855c580a){:target="_blank"} - $23.09

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=1491957662&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/1491957662/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491957662&linkCode=as2&tag=ledoux-20&linkId=eff92247940c967299befaed855c580a"){:target="_blank"}  This is a great book for learning the ins and outs of Pandas. It will teach you to clean, aggregate, transform, and visualize data in Python using Pandas dataframes. It's Python's closest equivalent to R for Data Science.


# Data Visualization

### 10. [The Visual Display of Quantitative Information -- Edward Tufte](https://www.amazon.com/gp/product/0961392142/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0961392142&linkCode=as2&tag=ledoux-20&linkId=a4446e84141df5df53f7ab70e9a8012f){:target="_blank"} - $32.95

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0961392142&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0961392142/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0961392142&linkCode=as2&tag=ledoux-20&linkId=a4446e84141df5df53f7ab70e9a8012f){:target="_blank"}  Communicating what your data have to say with clarity, precision, and efficiency. Its pretty graphics also make it a great coffee table book.

<br><br>

# Econometrics / Applied Statistics

### 11. [Mostly Harmless Econometrics: An Empiricist's Companion -- Angrist and Pischke](https://www.amazon.com/gp/product/0691120358/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0691120358&linkCode=as2&tag=ledoux-20&linkId=84446dd77a207550c2d4c965291326a6){:target="_blank"} [*HIGHLY RECOMMEND*] - $26.28

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0691120358&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0691120358/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0691120358&linkCode=as2&tag=ledoux-20&linkId=84446dd77a207550c2d4c965291326a6){:target="_blank"}  A handbook on advanced econometrics. Useful for brushing up on linear models (simple and multiple linear regression) and experiment design (instrumental variables, difference-in-difference models, answering causal questions.)

<br>

### 12. [Mastering Metrics: The Path from Cause to Effect -- Angrist and Pischke](https://www.amazon.com/gp/product/0691152845/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0691152845&linkCode=as2&tag=ledoux-20&linkId=9e21c69c2e45d3128382b6f74c8a2686){:target="_blank"} - $27.67

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0691152845&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0691152845/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0691152845&linkCode=as2&tag=ledoux-20&linkId=9e21c69c2e45d3128382b6f74c8a2686){:target="_blank"}  This book is very similar to Mostly Harmless Econometrics, but more beginner-friendly. Get this one instead if you're learning econometrics for the first time.

<br><br>

# Experiment Design

### 13. [Bit by Bit: Social Research in the Digital Age -- Matthew Salganik](https://www.amazon.com/gp/product/0691158649/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0691158649&linkCode=as2&tag=ledoux-20&linkId=4918b676a6a28e6628b95b7defdcf3cf){:target="_blank"} - $27.73

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0691158649&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0691158649/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0691158649&linkCode=as2&tag=ledoux-20&linkId=4918b676a6a28e6628b95b7defdcf3cf){:target="_blank"}  This book felt like a greatest hits compliation of all the most useful and exciting things I learned about experiment design as an undergrad. It's the best book I've found to date for marrying the strengths of old-school statisticians and newer-school data scientists. 

# Miscellanious (lighter reads)

### 14. [The Signal and the Noise — Nate Silver](https://www.amazon.com/gp/product/0143125087/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0143125087&linkCode=as2&tag=ledoux-20&linkId=4ac0969d9406eedf54fb3ac72c42c28a){:target="_blank"} - $11.28

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0143125087&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0143125087/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0143125087&linkCode=as2&tag=ledoux-20&linkId=4ac0969d9406eedf54fb3ac72c42c28a){:target="_blank"}  What is data science? How can it be used to solve real-world problems?

<br><br><br><br>

### 15. [The Book of Why -- Judea Pearl](https://www.amazon.com/gp/product/046509760X/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=046509760X&linkCode=as2&tag=ledoux-20&linkId=0e612597cb6a5b3594fdad9cf699bcc5){:target="_blank"} - $21.23

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=046509760X&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/046509760X/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=046509760X&linkCode=as2&tag=ledoux-20&linkId=0e612597cb6a5b3594fdad9cf699bcc5){:target="_blank"}  Learn the basics of causality

<br><br><br><br><br>

### 16. [The Information -- James Gleick](https://www.amazon.com/gp/product/1400096235/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1400096235&linkCode=as2&tag=ledoux-20&linkId=b2add85d410c261c11302314ecb7412e){:target="_blank"} - $13.98

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=1400096235&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/1400096235/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1400096235&linkCode=as2&tag=ledoux-20&linkId=b2add85d410c261c11302314ecb7412e){:target="_blank"}  A short, digestible history of and introduction to information theory. It won't make you an expert, but you'll get the main ideas.

<br><br><br><br>

### 17. [The Book: Playing the Percentages in Baseball - Tango, Lichtman and Dolphin](https://www.amazon.com/gp/product/1494260174/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1494260174&linkCode=as2&tag=ledoux-20&linkId=97bb3f6d906c705a6e8755a01ed1fd10){:target="_blank"} - $19.95

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=1494260174&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/1494260174/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1494260174&linkCode=as2&tag=ledoux-20&linkId=97bb3f6d906c705a6e8755a01ed1fd10){:target="_blank"}  Learn how data science has revolutionized the game of baseball, with plenty of applied examples using real data.

<br><br><br><br>

### 18. [Superforecasting: the Art and Science of Prediction — Phillip Tetlock](https://www.amazon.com/gp/product/0804136718/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0804136718&linkCode=as2&tag=ledoux-20&linkId=8f10f86aaf6ad911d57454c793cbc61b){:target="_blank"} - $13.11

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0804136718&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0804136718/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0804136718&linkCode=as2&tag=ledoux-20&linkId=8f10f86aaf6ad911d57454c793cbc61b){:target="_blank"} What makes a good forecast? See how a mix of quantitative and qualitative techniques can be combined to see the future.

<br><br><br><br>

### 19. [Chasing Perfection - Andy Clockner](https://www.amazon.com/gp/product/0306824027/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0306824027&linkCode=as2&tag=ledoux-20&linkId=a5df0ceb211536b22a3d8063f230a935){:target="_blank"} - $12.99

> [<img style="float: right;" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0306824027&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=ledoux-20">](https://www.amazon.com/gp/product/0306824027/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0306824027&linkCode=as2&tag=ledoux-20&linkId=a5df0ceb211536b22a3d8063f230a935){:target="_blank"}  A mostly-qualitative run through the current state of basketball analytics, detailing recent phenomena such as the decline of the mid-range jumper, tanking for draft picks, and the specialized medical analyses being used to ensure player longevity. 

