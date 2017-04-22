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

For the last analysis, I combined two different datasets together, which I fetched the sentiment_labelled_sentences from sentiment analysis library. This dataset include labelled sentences from amazon, IMDB and yelp. It is used to train my classifier.


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

First, let's see where the people care about the UA3411 incidents are from.</b>
1. Load data frame with processed location inforamtion from the tweets csv file
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample1.png" alt="sample1"/>
2. Extract the lattitudes and longintudes information from data frame
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample2.png" alt="sample2"/>
3. Draw a world's map using basemap. And use the location axis to draw on world's map.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/map1.png" alt="plot1"/>

<b>Conclusion:</b>People care about this incident are mainly from the United States. Many are from Asian. Most of them are from eastern of the United States where United Airline is mostly used for travel.

Then, about airlines and realated topics, what keywords are mentioned.</b>
1. Load data frame with processed location inforamtion from the tweets csv file.
2. Remove http:, punctuation, number, empty place and stop words from original data and put them in one list.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample3.png" alt="sample3"/>
3. Draw a word cloud picture to show the hottest words are mentioned about this incident.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/wordcloud.png" alt="plot2"/>

At last let's see people's habit of tweets</b>
1. Get what hour of a day that people tweet and count the number of them.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/sample4.png" alt="sample4"/>
2. Plot a figure to show the trend.
<img src="https://github.com/lishahan/INFO7374_PythonIntro_Final/blob/master/screenshot/habit.png" alt="plot3"/>

<b>Conclusion:</b>People tweet more in the evening. The peak time is 21:00-22:00 in a day.

## 2. User History and Relationship between Information




## 3. Trending of the UA3411 Incident and People's Attitude Using Sentiment Analysis

