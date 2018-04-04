# Technical Report for Capstone Project - The Mood of Music
Status: In progress

## How I acquired my data
I had different sources, here is a brief overview of how i acquired my data.<BR />

The 2 initial data sources were 2 data sets that I found on Kaggel:
- Spotify world wide daily song ranking:<BR /> 
https://www.kaggle.com/edumucelli/spotifys-worldwide-daily-song-ranking/<BR />
- Song lyrics:<BR /> 
https://www.kaggle.com/artimous/every-song-you-have-heard-almost/<BR />

I then had to add some more lyrics and more features.<BR />
- Additional song features from Spotify API (energy, mode, tempo, uri etc.)<BR />
https://developer.spotify.com/web-api
- Additional lyrics from Genius. Scraping through the API.<BR />
https://docs.genius.com/
- Last but not least I did add song lyrics by hand by googling the song to get the lyrics. 


## How the data should be transformed?
This project were made in different steps. I first did a MVP and then I added more data and did more models. 
And then again I did add more data and did more models. The data transformation was a little bit different 
from case to case. I will try to go over it here for each round.


### Data transformation before MVP
Cleaning the Spotify dataset from Kaggel:
- Create new columns for Year, Month and Day out of the Date column.
- The data ranges from January 1st 2017 to January 9th 2018. Remove the days in 2018, we only want to work with 
the data for 2017.
- Create a new column based on the different continents.
- Drop rows with missing values (mostly Track Name and Artist). It is nearly impossible to impute values for the 
2 columns, therefore dropping was the best option. The rows with missing values for the 2 columns were the same. 

Cleaning the Lyrics dataset from Kaggel:
- The data set were actually saved as 2 csv-files. I had to combined the 2 into one data frame to make the 
work easier.
- Drop rows were Song or Lyrics were missing. Extremely few. 
- Clean the data from '\r\n', '\n\n', '\r', '\n'.
- Make all the Lyrics into lower casing.

Combined the Kaggel Spotify data frame with the Kaggel Lyrics data frame. 
- In both data frames you will have to create a new column containing both the artist and song name. This is to 
make it possible to merge the 2 data frames together based on the newly created column. 

Combined the Kaggel Spotify+Lyrics data frame with Spotify API data frame. 
- Drop columns that are not going to be used:
'URL', 'art_song', 'Band', 'Song', '_merge', 'analysis_url', 'danceability', 'duration_ms', 'key', 'liveness',
'loudness', 'speechiness', 'time_signature', 'track_href', 'type', 'uri'.
- Drop rows that are duplicates. 

Combined the Kaggel Spotify+Lyrics+Spotify API data frame with Genius data frame.
- Make a new data frame only consisting rows of the top 8 music countries (US, UK, Germany, France, Canada,
Australia, Italy and the Netherlands.  

To the data frame for the top 8 countries add lyrics manually. Focus on the songs that appear the most frequently. Stop when you have lyrics for 68% or more of the songs. 

For the MVP I will only look at the column that will not change for a song on different rows, that is for example
characteristics for the song. That also means that we have to drop the columns that do change. The columns 
dropped were: 'Position', 'Streams', 'Date', 'Year', 'Month', 'Day', 'Country', 'Region'.

Use TextBlob on the Lyrics column to get 2 new columns for Polarity and Subjectivity.

Train/Test-split -> EDA -> MVP Model


### Data transformation before Good model
Same steps as for the MVP.

NLP
- Make list of stop words in English, French, German and Spanish.
- Develop the data frame into 2 new.
- Use CountVectorizer to get 1000 word features. Add them to the data frame.
- Use TF-IDF to get 1000 word features. Add them to another version of the data frame.

Train/Test-split -> EDA -> Good Model


### Data transformation before Better model
To the same things as for Good model, but instead of doing it for all countries at once, do it for each 
8 countries separately. 

Train/Test-split -> EDA -> Better Model


### Data transformation before Best model
Do the same things as for the MVP. But stop before you drop the columns that may change for a song on 
different rows. 

- Get dummies for the 8 countries.
- Get dummies for the position column.
- Group by the column ID and summarize the rows together that are grouped. 
- Create an average streams column.
- Create an average position column.
- Drop duplicates.
- Drop columns that before might changed per song (per row)
- Put all the new columns into the data frame consisting of the 8 countries and the columns that would not 
change per song (per row): 'Position', 'Streams', 'Date', 'Year', 'Month', 'Day', 'Country', 'Region'.
- Drop rows with missing values in the Lyrics column.

Use TextBlob on the Lyrics column to get 2 new columns for Polarity and Subjectivity.

Train/Test-split -> EDA -> Best Model


### Data transformation before Best model per countrie
Do the same thing as for Best model but split the data into data for each country. 



## How you operationalized your outcome variable? (including your justification)



## What models did i choose and what hyperparameters, including what metric or metrics you use to determine a successful model.

I knew that I needed to use a regressor of some kind. So I ended up using 5 different regressors in total. Before running the models I did use standard scaling in the case that scaling was needed. The Random Forest example do not need scaling before. 

### Linear Regression
Hyper params: N/A<BR />
Evaluation metric: R2, MSE

### Lasso Regressor
Hyper params<BR /> 
Tuned: alpha, selection<BR />
Tuned with both GridSearchCV and RandomizedSearchCV<BR />
Pre-chosen by me: random_state=24, fit_intercept=True, normalize=False, max_iter=1000<BR />
For the rest the default values were used.<BR />
Evaluation metric: R2, MSE

### Random Forest Regressor
Hyper params<BR />
Tuned: n_estimators, max_depth, max_features, bootstrap, verbose<BR />
Tuned with RandomizedSearchCV (due to time restraints)<BR /> 
Pre-chosen by me: random_state=24<BR />
For the rest the default values were used.<BR />
Evaluation metric: R2, MSE

### Ada Boosting Regressor (base estimator = DecisionTreeRegressor)
Hyper params<BR />
Tuned: n_estimators, loss<BR />
Tuned with RandomizedSearchCV (due to time restraints)<BR />
Pre-chosen by me: random_state=24<BR />
For the rest the default values were used.<BR />
Evaluation metric: R2, MSE

### Gradient Boosting Regressor
Hyper params<BR />
Tuned: n_estimators, loss, max_depth, max_features, verbose<BR />
Tuned with RandomizedSearchCV (due to time restraints)<BR />
Pre-chosen by me: random_state=24<BR />
For the rest the default values were used.<BR />
Evaluation metric: R2, MSE


## Any future deployment strategies, additions of data, or modeling techniques have I yet to try?
If there could have been more time I would have choosen to add in more data to try to see if it was possible
to improve the quality of the predictions. If not I would probably change the target. To predict the mood 
of a song seems to be hard. You do not have to use the mode to connect the song with an artist and the song 
to a country for to see if the artist is a good fit with a country. There are probably better variables to 
choose. I would definatly take some time to look at what those might be. 