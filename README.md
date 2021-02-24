# Trump Tweets vs. Approval Rating ETL

## Summary ##

This project extracted, transformed and loaded President Trump's tweets and compared them to his approval ratings at the same point in time. Hypothetically, the results could be useful to a campaign manager or agency interested in observing how a candidate or politician's tweets affect public reaction and ultimately impact the major population's approval of the candidate. 

We decided SQL would be the best ending format for our relational database, so our goal was to create CSV's for all individual datasets and load them into PostgreSQL. 

The first dataset we found was a list of approval ratings in the form of a csv.file on https://projects.fivethirtyeight.com/trump-approval-ratings, but the data started in 2017 and we wanted to include 2016 ratings. We pulled 2016 ratings from https://www.realclearpolitics.com/epolls/other/trump_favorableunfavorable-5493.html#polls and used pandas read_html function to parse the url, then cleaned the data and saved to a csv file. 

Next we wanted to pull actual Twitter info: ids, dates, retweets, favorites, etc. In order to add more complexity in our data extraction, we decided to each attempt one way of pulling tweets from Twitter. 

Michelle: My initial attempt was to parse Donald's twitter page using beautiful soup and splinter/selenium. After trying multiple versions of code with no success, I moved on to try the same code on a couple other webpages that had less tweets, thinking the notebook was overwhelmed. It turns out Twitter has barriers preventing complete visibility to the tweet's code and thats was what was causing the error. Even the other webpages were subliminally referring to Twitter's html. I ended up finding and dowloading a json file with Trump's tweets from 2016 and called it a day. I transformed the file into pandas dataframe, cleaning and renaming the data in order to merge with Kiran's. 

Kiran: Scraping President Trump’s tweets from Twitter in Python was the most direct way of extracting our raw data. Our main objective was to compile a comprehensive database of Trump’s tweets both during his presidency and his 2016 presidential campaign. There are two libraries that allow you to do this: Tweepy, which uses Twitter’s API and GetOldTweets3 which simply queries tweets. Both require simple pip installs. Tweepy relies on the standard API that only allows for tweets up to 7 days ago to be extracted. Whereas GetOldTweets3 allows for larger amounts of tweets and tweets older than a week to be retrieved. Thus it was suitable for our data extraction. I utilized the install to build a query based on Trump’s specific Twitter username and the desired date span. A list comprehension was compiled to specify which tweet data was pertinent, which was then assembled into a Pandas data frame. The data frame was then saved as a raw tweet CSV file. 

Pandas was then used again to read the CSV file and transform the data into a format that was useable for our considerations. The cleaned-up data frame was then saved as a separate output CSV file to be concatenated with our data frame containing Trump’s tweets from 2016. Once concatenated, the comprehensive CSV file was ready to imported into our SQL database.

We loaded our CSV files into a SQL database constructed of three tables. The relational aspect of the database is illustrated by how the tables have foreign keys that reference the primary key of the other table. 

While the end visual of our ETL project looks fairly simple, it took a lot of attempts and failures in data extraction, which turned out to be a real learning process!

---

## Data Sources ##
* https://twitter.com/realDonaldTrump
* https://github.com/bpb27/trump_tweet_data_archive
* https://projects.fivethirtyeight.com/trump-approval-ratings
* https://www.realclearpolitics.com/epolls/other/trump_favorableunfavorable-5493.html#polls

---

## Technologies Used ##
* PyCharm - Python IDE
* Jupyter Notebook
* Python - Pandas, JSON, NumPy, Datetime, GetOldTweets3
* PostgreSQL
* pgAdmin 4 - PostgreSQL IDE

---

## Authors ##
Kiran Rangaraj and Michelle Crawford Hannah - Vanderbilt University 2020
