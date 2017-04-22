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

I saved the CSV files locally which downloaded from NYC government and use two of these raw data as data sourses. <b>The reason why I use just two files not all of them, first is because that each file is really big, which takes time to run the code. Secondly, visualization of one file's data is just perfect, more data will make it looks unclearly.</b>

- Taxi-Green/2015-06.csv (size: 64.7M; row: 399,999)
- Taxi-Yellow/2015-06.csv (size: 45.6M; row: 399,999)

The reason these two files have the same rows is because I reduce the original 2GB+ file by using shell commond which split files by specific number of lines<br>

> split -l 400000 file name

The content of these two files are like below:

<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis1_1.png" alt="Analysis_1_1"/>
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis1_2.png" alt="Analysis_1_2"/>
New data frame after cleaning
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis1_5.png" alt="Analysis_1_5"/>

Pick out the data we need:
>pydf = ydf[['pickup_latitude','pickup_longitude']]<br>
>pgdf = gdf[['Pickup_latitude','Pickup_longitude']]

I made the following scatter plots of the pickup locations for the yellow cabs and green cabs. There were many outliers outside New York's five boroughs, so I restricted the box to more tightly contain the box of New York city limits as stated here. The box determined by this source has：
  <br>Lat/Lon Northwest: 40.917577, -74.25909
  <br>Lat/Lon Southeast: 40.477399, -73.700009

I used the box with the following corners for my scatter plots:
  <br>Lat/Lon Northwest: 40.997577, -74.259090
  <br>Lat/Lon Southeast: 40.517399, -73.600272
  
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/NYC_Taxi_Pick_Up_Locations.png" alt="Analysis_1_5"/>

Also see the seperate results below:

<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis1_3.png" alt="Analysis_1_3"/>
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis1_4.png" alt="Analysis_1_4"/>

<b>Conclusion:</b>The Yellow Taxi are most active in Manhattan Area and JFK airport, while the Green Taxi are active all over Manhattan and cities around it. 


## 2. User History and Relationship between Information

We have seen the pick up location distribution of Yellow and Green Taxi in NYC are different, then I wondered how their tips look like according to the customers from different area and different trips. So I next compared the tip amount to the total amount for both two types of cab. 

The data set used in this analysis from the same two files from above:

- Taxi-Green/2015-06.csv (size: 64.7M; row: 399,999)
- Taxi-Yellow/2015-06.csv (size: 45.6M; row: 399,999)

Pick up the data we need:
>tiptotalamountsydf = ydf[['tip_amount','total_amount']]
>tiptotalamountsgdf = gdf[['Tip_amount','Total_amount']]   (titles in raw files are different)

I cleaned the data to only consider when the total amount was less than or equal to $200 to make the visualization more clear. 
>cleantiptotalamountsydf = tiptotalamountsydf.loc[tiptotalamountsydf['total_amount'].isin(range(1,201))]
>cleantiptotalamountsgdf = tiptotalamountsgdf.loc[tiptotalamountsgdf['Total_amount'].isin(range(1,201))]

Later, according to the real figure, I reduce the x,y scale as well.
>fig = plt.figure(figsize=(15,10))

To make data more readable, I add a scope line using <b>numpy least squares polynomial fit</b>, which finally shows the ratio when total amount change, how the tip goes. And I print the scope and Y-intercept out as well. <br>
least squares polynomial fit: https://docs.scipy.org/doc/numpy/reference/generated/numpy.polyfit.html

Here are the analysis result below:
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis2_1.png" alt="Analysis_2_1"/>
<b>Slope =  0.187226732214<br>
y-intercept =  -0.0048498151184</b><br>
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis2_2.png" alt="Analysis_2"/>
<b>Slope =  0.0535737315808<br>
y-intercept =  0.851370904574</b>

<b>Conclusion: </b><br>
Yellow Taxi: Most tips are in the range of total amount $1-$30, according to the scope, call mean value $15 in, we got <b>$2.80</b> is the average tips for yellow cab drivers.<br>
Green Taxi: Most tips are in the range of total amount $1-$40, according to the scope, call mean value $20 in, we got <b>$1.07</b> is the average tips for green cab drivers.<br>
So we see the reason why yellow taxi and most green taxi drivers are like to hang around within Manhattan Area. Shorter trips, but higher tips. (SMART choice) From Chris Whong's “a day in the life of a NYC taxi”, we can also easily find that although trips in Manhattan are really short and won't cost customers over $20 most of time, taxi drivers can still receive around $650 per day, and $50 tips.<br>


## 3. Trending of the UA3411 Incident and People's Attitude Using Sentiment Analysis

After we know the reason why NYC Taxi driver love Manhattan, now let us focus on this magic area. In this question I picked Yellow Taxi as my target only, since their action are mostly in this area, and we can get most accurate result with its data. <br>
This time I use the data in another file: (since the data in 2015-06 only do not contain weekend data after reducing)

- Taxi-Yellow/2014-07.csv (size: 42M; row: 399,999)

Pick up the data we need: 

>pydf = ydf[[' pickup_datetime',' passenger_count']]

According to the date, add day format using datatime to a new column and generate a new CSV file.

<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis3_1.png" alt="Analysis_3_1"/>

Get each hour's passenger average total count by each specific day.

<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis3_2.png" alt="Analysis_3_2"/>
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis3_3.png" alt="Analysis_3_3"/>

Create a new Data Frame contain just 24 hour and passenger count.

<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis3_4.png" alt="Analysis_3_4"/>

Generate line plot for weekday and weekend visualization.
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis3_5.png" alt="Analysis_3_5"/>
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis3_6.png" alt="Analysis_3_6"/>

Finally, I created a bar plot to show the whole weeks passagers count by add each day's 24 hours' value together.
<img src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis3_7.png" alt="Analysis_3_7"/>

<b>Conclusion: </b><br>
During the weekday, taxi business always warms up after around 6:00 AM until 6:00 PM, when they will face their busiest 5 hours to 11 PM. Passenger number will be doubled on Thursday and Friday. So we see that New York people have a colorful nightlife. <br>
During the weekend, taxi business last almost the whole day, and will reach the peak at 12:00 midnight, and down to the bottom at 5:00 AM. 


## 4. NY Taxi (Green) trips change during snowfall days

For practicing cross data analysis, this time I want to see how different weather influence NYC Taxi business. 
I downloaded daily Central Park weather data from the National Climatic Data Center, and joined it to Green Taxi data to see if we could learn anything else about the relationship between weather and taxi rides. I picked Green Taxi because their active area are much bigger than the Yellow Cabs as we seen in the first question.

First I read the Green Taxi CSV file from 2014-04 to 2015-04, and also the weather data also from 2014-2015.

<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis4_1.png" alt="Analysis_4_1"/>
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis4_2.png" alt="Analysis_4_2"/>

Then I started to pick the data I need and format the data frame for later connection.<br>
I picked Passenger Count from Taxi data and Humidity, Windspeed, Snowdepth from weather data.<br>
I want to see how Rain, Windy, and Snowy day influence Taxi business.

>new_df = df1.loc[:,['lpep_pickup_datetime','Passenger_count']]
>joint_df['date'] = joint_df['lpep_pickup_datetime'].apply(lambda x: datetime.strptime(x,'%m/%d/%y %H:%M').date().strftime('%m/%d/%y'))<br>
>df1 = new_g_df.groupby(['date']).sum()

>new_w_df = w_df.loc[:,['HOURLYRelativeHumidity','HOURLYWindSpeed','DAILYSnowDepth','date']]
>df2 = new_w_df.groupby(['date']).mean()

<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis4_3.png" alt="Analysis_4_3"/>

<b>Merge</b> two datasets by 'date' column I created.
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis4_4.png" alt="Analysis_4_4"/>

Now it is time to find out which days are rainy day, windy day or snowy day. And get related passenger count.
>rain_df = new_df[new_df['HOURLYRelativeHumidity']>75]
>rain_df['Weather Condition'] = pd.Series('Rain', index=rain_df.index)
>rain_df = rain_df.loc[:,['Weather Condition','Passenger_count']].reset_index(drop=True)
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis4_5.png" alt="Analysis_4_5"/>

Finally, we can create a boxplot to see the passenger count in different weather condition, and I set <b>good weather day</b> as a reference substance to see the difference. 
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis4_6.png" alt="Analysis_4_6"/>

<b>Conclusion: </b> In rainy and windy day, the average number of passengers of green taxi are higher than good weather days, while in snowy day this mean number is lower than normal days. Even no riders at all during snow stom (over 10 Inch)

## 5. Does Uber's raise influence NY Taxi career.

When Green Taxi appeared in NYC, it brought Yellow Taxi a big impact surround Manhattan Area, let us see an visualization analysis created by Todd W. Schneider recently first.

<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis5_1.png" alt="Analysis_5_1"/>

Now I am trying to find out the impact from Uber to NYC Yellow or Green Cabs. There is some publicly available data covering nearly 19 million Uber rides in NYC from April–September 2014 and January–June 2015, which I’ve incorporated into the dataset.

The data are downloaded from http://www.nyc.gov and fivethirtyeight's github shared datasets. Since the each data is over 2GB, I have to reduced them with necessary data and generate CSV files for later use (400MB+ still too big to upload to the github). I can only update some secondly reduced data to the github which is less than the 25MB limitation. 

I am trying to dynamically generate the analysis figures by using <b>argparse</b>, which allow you to input the cities names in New York Area. And I did little research on city zone longitude and latitude on Google Maps. Below listing the New York cities names and their coordinate ranges.<br>

| City Name| Longitude | Latitude |
| ------------ | ------------- | ------------- |
| Manhattan | -74.016309 ~ -73.943986 | 40.703363 ~ 40.822683 |
| Brooklyn | -73.996224 ~ -73.904354 | 40.590195 ~ 40.699933 |
| Queens | -73.929015 ~ -73.732468 | 40.667349 ~ 40.782815 |
| Bronx | -73.909672 ~ -73.814439 | 40.805118 ~ 40.910298 |
| Staten Island | -74.241142 ~ -74.093445 | 40.506272 ~ 40.643899 |
| JFK Airport | -73.815939 ~ -73.764694 | 40.636008 ~ 40.662522 |

First, begin the data cleaning, pick out the pickup coordinate only, unique the columns name of all files, remove all empty rows and out put CSV files for later use. 

>df = df.loc[:,['pickup_longitude','pickup_latitude']]
>df.columns = ['Longitude', 'Latitude']
>df = df[(df.T != 0).any()]

Dealing with Uber 2015 dataset: Uber 2015 data is different from Yellow/Green Taxi and Uber 2014 data, it does not contain Longitude and Latitude columns, instead, it hold <b>locationID</b> which refer to New York cities. I found a locatonID-borough comparison table on http://www.nyc.gov and left merge it to 2015 Uber dataset.

Difference between 2014 Uber data and 2015 Uber data. locationID-borough comparison table.
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis5_2.png" alt="Analysis_5_2"/>

New data set after merging two tables
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis5_3.png" alt="Analysis_5_3"/>

Define a function to deeply reduce the data of each file according to input city parameter. Then get each month trips count and put it in a new data frame for visualization purpose. 
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis5_4.png" alt="Analysis_5_4"/>
Also create a static method to generate the figure without any input.
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis5_5.png" alt="Analysis_5_5"/>

Below are two analysis figure for Manhattan and Brooklyn.
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis5_6.png" alt="Analysis_5_6"/>
<img
src="https://github.com/TIANJIESONG/Python_GitHub/blob/Tianjie_Song_Assignment_1_000315585/Uber%26Taxi_NY_Data_Analysis/screenshot/Analysis5_7.png" alt="Analysis_5_7"/>

<b>Conclusion: </b>Uber has grown dramatically in Manhattan, notching a 275% increase in pickups from June 2014 to June 2015. Uber made 1.4 million more Manhattan pickups in June 2015 than it did in June 2014, while taxis made 1.1 million fewer pickups. However, even though Uber picked up nearly 2 million Manhattan passengers in June 2015, Uber still accounts for less than 15% of total Manhattan pickups. Same situation happens in other cities as well.<br>
<b>Is Uber's time coming? We will see in the near future!</b>


