# Capstone Project - The Mood of Music Around the Globe
The Capstone Project is my final project from my Data Science Immersive program experience at General Assembly. 
Key element in the project had to be:
- Develop an interesting question
- Collect the data required to model that data
- Developing the strongest model(s) for prediction
- Communicat the findings to other data scientists and non-technical individuals. 


## Description and target
**Phase 1**
For this project my goal is to see if happy, neutral or sad songs will be the most popular in a specific country. The mood of the song can be decided based on lyrics.(I will start with focusing on one region of the world.)

**Phase 2**
I will see if the mood of the top songs can determine other factors of a country (Political situation, cultura exports, population etc.) 

**Phase 3**
I will try to recommend songs based their mood similarities to other songs. (If you like this song, you will probably like this song.)


## The Data
**Initial data**<BR />
Spotify world wide daily song ranking:<BR /> 
https://www.kaggle.com/edumucelli/spotifys-worldwide-daily-song-ranking/<BR />
Song lyrics:<BR /> 
https://www.kaggle.com/artimous/every-song-you-have-heard-almost/

I think I will have to scrape some data. Because I have a feeling that some songs might be missing in the lyrics data.

For phase 2 I will have to look for other data sources. I have seen suitable data sets, so I just have to decide on what other factors to look at. 


## Tools (initial thoughts)
- Clustering (K-means)
- NLP
- TextBlob 
- Model evaluation


## Jupyter Notebook 1 - cleaning_top_songs
This notebook include: 
- Loading the data
_ Looking at the data
- Initial munging and EDA (in progress)


## Jupyter Notebook 2 - cleaning_lyrics
This notebook include: 
- Loading the data
_ Looking at the data
- Initial munging and EDA (in progress)


## Jupyter Notebook n
There will be more Jupyter Notebooks.

The next step is combine the top songs and the lyrics to one dataframe.
(Here I will also do a train test split on the data.)
I will then do more munging and EDA on that data.
Then comes the modeling and tuning.
And in the end the concution and presentation.

I will update this document as the project progresses.


## This is a working copy
The project is still active and not finnished yet.
So please keep that in mind. 
