# a3

How to run part A:
1) open 3 terminals in file location
2) For terminal 1: 
    - docker run -it -v $PWD:/app --name twitter -w /app python bash
    – pip install -U tweepy
    – python twitter_app.py
3) For terminal 2:
    - docker run -it -v $PWD:/app --name dashboard -w /app python bash
    - python app.py
4) For terminal 3:
    – docker run -it -v $PWD:/app --link twitter:twitter --link dashboard:dashboard eecsyorku/eecs4415
    – spark-submit spark_app.py

How to run part B:
1) open 3 terminals in file location
2) For terminal 1: 
    - docker run -it -v $PWD:/app --name twitter -w /app python bash
    – pip install -U tweepy
    – python twitter_app.py
3) For terminal 2:
    - docker run -it -v $PWD:/app --name dashboard -w /app python bash
    - python app.py
4) For terminal 3:
    – docker run -it -v $PWD:/app --link twitter:twitter --link dashboard:dashboard eecsyorku/eecs4415
    - pip install nltk
    - python (go into python bash)
    - import nltk
    - nltk.download('vader_lexicon')
    - exit
    – spark-submit spark_app.py


Note: 
If one is re-running a docker image you can restart old docker image by:
1) Checking for list of docker: docker container list -a
2) docker run "nameofDockerImage"
3) docker exec -it "nameofDockerImage" bash

In case there are errors installing nltk libraries:
apt-get update
apt-get install gcc
apt-get install python-dev python3-dev
apt-get install python-nltk
  
  
  
  
  
  A. Identifying Trendsin Twitter (60%)Twitter is one of the main online social networks where users post and interact with messages known as "tweets".Tweets  allow  for  instant,  short,  and  frequent  communicationand  they  have  been  proved an effective way  to  communicate newsand  other  timely  information.  Therefore,  a  practical  use  for Twitter's functionalityis to be used for identifying trends in real-time.Identifying trends is important for severalindustries and services, including marketing, customer service, and crisis response.Your  task  is  to  design  and  implement  a  Twitter  streaming  application  that tracks  specific  hashtags  and reports their popularity (# occurrences) in real-time.In particular, you need to:•Identify 5 related #hashtags (e.g., political parties, companies, product brands, stocks, etc.)•Collect tweets mentioning any of the 5 #hashtags in real-time•Compute the number of occurrences of each of the mentioned hashtags•Plot the results of your analysis in real-time. Alternatively, you can decide to store the results in a  file,  post-process  them as  a  batch  (offline) and  create  a  plot  based  onthe  post-process analysis.The  results  are  based  on  the time  window  that  your  application  is running(from the time it begins, until it is killed or interrupted/stopped).For  the  needs  of  your  assignment,  you  will  need  to  stitchtogether  a number  of  technologies  that  can enable the analysis to be performed, including:A  Twitter  client:  This  is  an  application  that  connects  to  the  Twitter  service  and  obtains  tweets  as  they become available. It requires to create your own credentials to access the Twitter APIs.See Appendix A.Apache  Spark  Streaming: This  is  an apache spark streaming application  that connectsto yourtwitter client,  receivesthe  tweets as  a  stream, performs real-time  processing of the  incoming  tweets,  extractsuseful information, and computes the quantities of interest (i.e., number of occurrences of a #hashtag).Real-time reporting: This is a visualization component that reports through a plot the results computed by   the   apache   spark   streaming   application   in   real-time.   This   can   be   implemented   using   AJAX (asynchronous HTTP calls); see the resources of the Appendix B for examples. Alternatively, results can be stored in a file in real-time, post-processed as a batch (offline), and presented as a plot.Notes: •Severalimplementation  approaches exist  for  this  application.  You  are  encouraged  to  make assumptions, make decisions  and  follow  the  technical  path  that  you  feel  is  more  appropriate. You will have a chance to explain your approach during the marking session•Appendix A provides instructions on how to setup a Twitter application•Appendix B provides severalonline resources related to the assignment
B. Real-time Sentiment Analysis of Twitter Topics (40%)In  the  field  of  computational  linguistics  and  natural  language  processing, sentiment  analysisaims  to determinethe attitude of a speaker, writer, or other subject with respect to some topic or the overall contextual  polarity  or  emotional  reaction  to  a  document,  interaction,  or  event.A  basic  task  in sentiment   analysis   is   classifying   the polarityof   a   given   text   at   the   document,   sentence,   or feature/aspect   level—whether   the   expressed   opinion   in   a   document,   a   sentence   or   an   entity feature/aspect is positive, negative, or neutral.For example, consider the following three text inputs:“I love ice cream a lot”“I dislike ice cream a lot”“ice cream is made from milk”One would expect that the polarity of the first is (rather) positive, of the second is (rather) negativeand of the third is (rather) neutral. The word “rather”is used here to express subjectivity, since humans not always  agree  about  the  polarity  of a  sentence.We  rely  onan  out-of-the-shelf  library  to  perform sentiment analysis.The analysis will be on the level of a document, where the document is a tweet (i.e., all the words in a single tweet).Your  task  is  to  design  and implement a Twitter streaming  application that performs  sentiment  analysis of tweets related to competitive topicsand provides a real-time monitoring of the polarity.•Identify 5 competitive topics (e.g., political parties, companies, product brands, stocks, etc.)•Manually select a set of 10 hashtags that better describeeach of the topicidentified above•Collect tweetsrelated to the 5 topics in real-time and perform sentiment analysis for eachtopic•Plot the results of  your  analysis  in  real-time.  Alternatively,you  can  decide  to store results  in  a file, post-process themand create a plot based on the post-process analysisNotes:•The  implementation  approach  for  the  streaming  application  should  be similar  tothe  one followed in Part A•For the sentiment analysis you should employ Python’s Natural Language Toolkit (NLTK)library•Appendix A provides instructions on how to setup a Twitter application•Appendix B provides several online resources related to the assignment
Appendix A –Setting up a Twitter Application& Installing TweepyTo start collecting tweets, you need to set up a Twitter application and get credentials that allow you to pulltweets out of the twitter streaming API.Then, you need to develop a Twitter client that connectsto Twitter and acquires Twitter data. You can do that using Tweepy. Create a Twitter Applicationand Obtain OAuthAccess KeysBriefly, you need to:•Create a Twitter developer account: https://developer.twitter.com/en/apply-for-access•Create a New Application•Fill in your Application DetailsoName: Your app name. It needs to be a unique name across all twitter applicationsoDescription: Ashort description for your appoWebsite: The website address where the app will be hosted. Use a placeholder for nowoCallback URL: Ignore this field•Create Your Access Token•Choose what Access Type You Need (choose 'Read only')•Make a note of your OAuth Settings, including Consumer Key, Consumer Secret,OAuth Access Token,OAuth Access Token SecretYou should keep these secret, since anyone with thekeys, could effectively access your Twitter account.Detailed information is provided in the links below (and other resources similar online).•Create your own Twitter App: https://smashballoon.com/doc/create-your-own-twitter-app/•Twitter  Tutorial: Step-by-step  guide  to  making  your  first  request  to  the  new  Twitter  API  v2:https://developer.twitter.com/en/docs/tutorials/step-by-step-guide-to-making-your-first-request-to-the-twitter-api-v2Install TweepyTweepyisa python library for accessing the Twitter API. You can install Tweepy using pip:$pip install tweepyYou may also use Git to clone the repository directly from Github and install it manually:$git clone https://github.com/tweepy/tweepy.git$cd tweepy$python setup.py installThe next step is to use Tweepy to createa Twitter application that usesyour Twittercredentials.More information: https://github.com/tweepy/tweepy
Appendix B–Useful Online Resources and TutorialsSpark Streaming Programming Guidehttp://spark.apache.org/docs/latest/streaming-programming-guide.htmlPython Streaming Exampleshttps://github.com/apache/spark/tree/master/examples/src/main/python/streamingAn easy-to-use Python library for accessing the Twitter APIhttp://www.tweepy.org/Tutorial on Medium: Apache Spark at a Glancehttps://medium.com/cloudnesil/apache-spark-at-a-glance-7088b9fe5ef5Apache Spark General Tutorialhttps://www.toptal.com/spark/introduction-to-apache-sparkApache Spark Streaming Tutorial: Identifying Trending Twitter Hashtagshttps://www.toptal.com/apache/apache-spark-streaming-twitterApache Spark Streaming with Twitter (and Python)https://www.linkedin.com/pulse/apache-spark-streaming-twitter-python-laurent-weichberger/Twitter-Sentiment-Analysis-Using-Spark-Streaming-And-Kafkahttps://github.com/sridharswamy/Twitter-Sentiment-Analysis-Using-Spark-Streaming-And-KafkaTwitter Sentiment Analysis using Pythonhttps://www.geeksforgeeks.org/twitter-sentiment-analysis-using-python/Sentiment Analysis on Reddit News Headlines with Python’s Natural Language Toolkit (NLTK)https://www.learndatasci.com/tutorials/sentiment-analysis-reddit-headlines-pythons-nltk/
