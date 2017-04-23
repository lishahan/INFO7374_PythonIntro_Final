# Data Analysis with the UA3411 Overbooking Incident

## Introduction

I want to take a deep data analysis tour at my final project. This is challanging with big dataset, new api and sentiment analysis. I will not only use all of what professor taught us from the course and I will also learn more packages and introduction of machine learning.

I chose the twitter search api and a recent popular incident as my dataset and theme. Sentiment analysis is always attracted to me. Combination of sentiment analysis and tweets is a good model to show the trend and every turning point of this incident. If I dig deeper about users' information I will get more interesting discovery about relationship between user and twitter. 

Here is a little bit backgroud of this incident:
On the United Express Flight 3411 scheduled for April 9, 2017 just before 5:20 p.m., O'Hare International Airport police forcibly removed passenger David Dao from the aircraft after he refused to depart the airplane upon the demand of management. Dao screamed as officers pulled him out of his seat, and his face hit an armrest during the struggle. Officers then dragged him, apparently unconscious, by his arms on his back along the aircraft aisle past rows of onlooking passengers. He was later seen with blood around his mouth. Prior to the confrontation, managers offered compensation to passengers to vacate their seats to make room for four airline employees who needed to travel to the destination, Louisville International Airport, but none of the fliers accepted. Four passengers were then selected for involuntary removal from the flight. Three other passengers complied, and Dao was selected to be fourth. Republic Airline operated the scheduled passenger flight on behalf of United Express, a United Airlines regional branch.
Video of the incident recorded by passengers went viral on social media, resulting in outrage over the violent incident. Politicians expressed concern and called for official investigation. U.S. President Donald Trump criticized United Airlines, calling treatment of their customer "horrible".<br/>


## Analysis Questions

My researh topics are:<br/>
1. Distribution map of tweeters, word cloud of hot tweets and hour of a day people tweets<br/>
2. Deep analysis of user information relationships<br/>
3. Trending of the UA3411 incident and people's attitude using sentiment analysis<br/>


## Data Collection

I used the Twitter Search API to fetch the latest tweets. 

The keywords I use is mainly about the recent UA3411 incident. 100 tweets per .json file. The UA3411 Incident happened on Apr 9th 2017. Timing is perfect. I get data from Apr 7th to current date to make comparison. Since the Twitter Search API only provide tweets from the past week and 450 request per 15mins, I request data many times a day. 

For the last analysis, I combined many different datasets together. One of thme is the data I fetched the sentiment_labelled_sentences from sentiment analysis library. And one of them is the NLTK movie review libiray. These datasets include labelled sentences from amazon, NLTK movie reviews, IMDB and yelp. It is used to train my classifier.


## Data Storing

To make sure there is no data overwrite, I saved each .json file with its query and an unix timestamp. I catagorize the .json files in folders named by its keywords and they will be catagorized by time

Here is the how my download data file looks like.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/datafolder.png" alt="Data_1"/>
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/data_hi1.png" alt="Data_2"/>
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/data_h2.png" alt="Data_3"/>
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/json_timestamp.png" alt="Data_4"/>


## Data Processing

I extract all the tweets I collected from the raw data and store them as a list in a .json file. Get the information of users info, tweets, location, country and other data I will use in the future analysis and store them in a .csv and a .txt file.

<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/data_clean.png" alt="Data_5"/>


## Analysis Details

## 1. Distributions of Tweeters and Tweets of the UA3411 Incident

### First, let's see where the people care about the UA3411 incidents are from.</b>
1. Load data frame with processed location inforamtion from the tweets csv file
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample1.png" alt="sample1"/>
2. Extract the lattitudes and longintudes information from data frame
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample2.png" alt="sample2"/>
3. Draw a world's map using basemap. And use the location axis to draw on world's map.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/map1.png" alt="plot1"/>

<b>Conclusion:</b>People care about this incident are mainly from the United States. Many are from Asian. Most of them are from eastern of the United States where United Airline is mostly used for travel.

### Then, about airlines and realated topics, what keywords are mentioned.</b>
1. Load data frame with processed location inforamtion from the tweets csv file.
2. Remove http:, punctuation, number, empty place and stop words from original data and put them in one list.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample3.png" alt="sample3"/>
3. Draw a word cloud picture to show the hottest words are mentioned about this incident.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/wordcloud.png" alt="plot2"/>

### At last let's see people's habit of tweets</b>
1. Get what hour of a day that people tweet and count the number of them.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample4.png" alt="sample4"/>
2. Plot a figure to show the trend.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/habit.png" alt="plot3"/>

<b>Conclusion:</b>People tweet more in the evening. The peak time is 21:00-22:00 in a day.

## 2. User History and Relation between Information

In this analysis. I want to find out more relation between user history and retweets. I always thought older user got more followers. Older user gets more retweets. But no data no talk. Will these discoveries subvert what we thought? Let's see my discoveries.

### Let's see the relationship between user history and retweet count. </b>
1. Load data from processed .csv file.
2. Get the information of retweet, user created time, user name and follower count.
3. Get rid of duplicated tweets by text.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample5.png" alt="sample5"/>
4. Get when users are created.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample6.png" alt="sample6"/>
5. Group retweet count by year.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample7.png" alt="sample7"/>
6. Plot a fig to show the relation.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/relation1.png" alt="relation1"/>

<b>Conclusion:</b>The trending plot shows that older user doesnt't get much retweet. The count of retweets rises with time going. More recent created user got more retweet. The peak is year of 2014. This group of people are young and care about the trending news. They got more retweets than the other users. 

### Is the older the user is the more followers one has true? </b>
1. Group follower count by year.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample8.png" alt="sample8"/>
2. Plot a fig to show the relation.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/relation2.png" alt="relation2"/>

<b>Conclusion:</b>User created on 2007 got the most followers. This is because Twitter was created on 2016. User increased rapidly on 2017. But this number dropped after 2017. New user created on 2017 got less followers. According to this analysis. It makes sense that the older the user is the more followers.

### Does more followers brings more retweets? </b>
1. Group retweet and flower count by user name.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample9.png" alt="sample9"/>
2. Plot a scatter to show the relation.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/relation3.png" alt="relation3"/>

<b>Conclusion:</b>We can see the scatters groups at the beginnig of this plot. It is interesting that, according to this research, more followers doesn't bring more retweets. People care more about the meaning of what one tweet and choose to retweet the information they care about more.


## 3. Trending of the UA3411 Incident and People's Attitude Using Sentiment Analysis

In this analysis, I want to learn more about sentiment analysis and machine learning. I trained my own classifier and use is to analyze the attitude of each tweet. This is a long process. Took me a few days to train a good classifier. I found it can give me a right result of a false negative sentence. There are still some limitations. If I got more days, I will train a even more precise classifier.
I used NLTK movie reviews and the labeled sentenses library of yelp, amazon and IMDB to train it. Then I used a set of movie reviews to test my classifier's accuracy.
Through this research. We can see people's attitude towards this incidents. After this incidents the United Ariline took several public actions. It is very interesting to see how people talk about this incident. Let's see my discovery.

### Train a sentiment classifier and store it for future use. </b>
I use NaiveBayesClassifier to be my classifier. They are a family of simple probabilistic classifiers based on applying Bayes' theorem with strong (naive) independence assumptions between the features. No need to input too much parameters. You can use sentences with attitude label to train it. The sentence and the label you use should be a tuple. The more the more presise it will be.

1. Build trainer from nltk.corpus movie_reviews, positive&negative dataset from yelp and amazon.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample10.png" alt="sample10"/>
2. Train the classifier and save it as classifier.pickle for future use.

It is a process of machine learning. To train a good classifier, this process took a long time. The classifier is over 2GB on my disk. You can download it via the link I store in link_to_data.txt (https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/Data/link_to_data.txt).

<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample11.png" alt="sample11"/>
3. A little test of a false positive sentence.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample12.png" alt="sample12"/>

### Test the accuracy of classifier. </b>
There are several important parameters to reflec the accuracy of a classifier. I used positive and negative precistion, recall rate and f-measure metrics.
1. Build a tester.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample13png" alt="sample13"/>
2. Test the accuracy of my classifier.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample14.png" alt="sample14"/>

<b>Conclusion:</b>We can see the classifier's positive and negative presision are both over 90%. And the recall rate are low. That means my classifier's accuracy is not bad. I can use is for future sentiment analysis.

### Pick six related keywords of United Airline incident and see what people are complain or praise about. </b>
I chose severy keywords for this analysis. They are mainly about this incident and the serveice people care about an airline company. 

1. Get rid of the tweets that have nothing to do with these keywords.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample15.png" alt="sample15"/>
2. Catagories tweets by keywords. 
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample16.png" alt="sample16"/>
3. Use the trained classifier to check each tweet, 1 stands for positive and -1 stands for negative. Get the tweet date of each text. Add token for future caculation.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample17.png" alt="sample17"/>
4. Group the token by different keyword and attitude. Store the positive and negative attitude in two list.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample18.png" alt="sample18"/>
5.Plot a fig to see people's attitued of different aspect of UA's service.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/posandneg.png" alt="posandneg"/>

<b>Conclusion:</b>There are a lot more negative tweets than the positive ones. We can see people are negative about this incident. And the most negative tweets focus on the United Airline. 

### Use this well trained classifier to check the tweets from people. </b>
This research will show people's attitude trending by days. This will be reflected by the United Airline's public action. Through the trend we can see if these actions work.

1. Caculate people's attitude by day.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample19.png" alt="sample19"/>
2. Plot a fig to see the trend of people's attitued by day.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/posandneg1.png" alt="posandneg1"/>

<b>Conclusion:</b>Over this reserch, we can see that before Apr 4th 2017, there were not many tweets about this incident. After 9th, since the doctor got dragged down to the airplane video was widely spread, more and more people are tweeting about this incident. The negative tweets keeps rising cause the United Airline didn't apologise about this violent incident at all. The count of tweets may drop a little bit and the positive tweets rise a little because the CEO of the United Airline finally make an propriate apology about this incident on 16th Apr. After all, The negative tweets are still more than the positive tweets. This is not suprising. This may cause us to check its culture again. United airline does need a good public coordinator. Only better service can win customers. Maybe in the future most of the tweets about United Airline will be positive. 


## Thank you for reviewing my research. I did put lots of effort and thought in it. I havest a good practice and extention of all the knowlege of Python. Learned a lot from this course. Thanks again. 