# Calculation of TopN Hashtags in real time using Apache Storm
## Introduction
I have taken the course [ud381 - Real Time Analytics with Apache Storm](https://www.udacity.com/course/real-time-analytics-with-apache-storm--ud381)  on udacity in the summer of 2015. With it, I created a project that calculates trending hashtags on a twitter stream. The trending hashtags are shown as a word cloud on a web application powered by [Flask](http://flask.pocoo.org) and [d3.js](http://d3js.org/). The communication between Storm and the web application located in the viz folder, is done using [redis](http://redis.io).

## Steps to set up
Before you can run this project on storm, you will need some API keys that twitter provides. For that, an
account on the Twitter is needed. Further, an application is needed to be created on the platform
(https://apps.twitter.com/). With the application created, you get 4 authorization keys namely
* Consumer key
* Consumer secret
* Access token
* Access token secret

We are going to need all these in setting up a spout that will emit tweets. Now, open the file 
*src/jvm/anish/storm/TopNTweetTopology.java* In lines 39-40, you will see
```java
TweetSpout tweetSpout = new TweetSpout(
        "[Your customer key]",
        "[Your secret key]",
        "[Your access token",
        "[Your access secret]"
    );
```
Replace the fields with the respective keys that you have obtained from twitter. And yes, no square brackets should
be present in the arguments.

After you have completed this, time to compile your maven package. It will take some time depending upon your internet speed, or how many of the required packages you already have. I have used maven to compile this project. You can install maven using
```sh
sudo apt-get install maven 
```
For other platforms, [check out the project page](https://maven.apache.org/run-maven/index.html)

After you have installed maven, cd to the directory of the project, and compile the project using

```sh
mvn package
```

## Running the project
Make sure that you have installed storm and is accessible using **storm** command in the shell.More information about Apache Storm [here](http://storm.apache.org). Once the project is compiled, you can see a new directory called **target** is created in the root folder.
Fire up the web application by navigating to the **viz** folder and running the app.py file
```
python app.py
```

Now, execute the storm topology using:
```sh
storm jar target/anish-storm-0.0.1-SNAPSHOT-jar-with-dependencies.jar anish.storm.TopNTweetTopology
```
See the topology running, and word cloud on your web application page at
**http://localhost:5000/***
