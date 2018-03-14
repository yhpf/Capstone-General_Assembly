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
Status: first version done

This notebook include: 
- Loading the data from csv-file
- Get to know the data & some initial fix
- Save data to new csv-file<BR />

### Get to know the data & some initial fix
- Looked at entire df<BR />
	Shape: (3441197, 7)<BR />
	Columns: Position, Track Name, Artist, Streams, URL, Date, Region

		Position
		- No missing values
		- Data type integer64

		Track Name
		- 657 missing values (rows was removed)
		- Data type string
		- Comment: I might want to decide not to use data from the Asian region since they have Artists 
		and Track Names in foreign signs. I did choose to remove the rows with missing values bc I came 
		to the conclusion that it would be impossible to fill them in with other values. 657 rows out of 
		3441197 are also very few and they seemes to be distributed over different regions.

		Artist
		- 657 missing values (rows was removed, same rowes as for Track Name)
		- Data type string
		- Comment: I might want to decide not to use data from the Asian region since they have Artists 
		and Track Names in foreign signs. I did choose to remove the rows with missing values bc I came 
		to the conclusion that it would be impossible to fill them in with other values. 657 rows out of 
		3441197 are also very few and they seemes to be distributed over different regions.

		Streams
		- No missing values
		- Data type integer64

		Date
		- No missing values
		- Data type string (was converted into datetime)
		- 3 new columns created for Year, Month, Day
		- There was data from 1 jan 2017 to 9 jan 2018. I removed the 9 days from 2018. I only want data 
		for 2017.

		Region
		- Column renamed to Country
		- No missing values
		- Data type string
		- A new column (Region) was created featuring groups of countries, based on what continent they 
		belong to.
		- Comment: I did find a dictionary for what country each letter combination was exual to. (Is saves 
		in the file contry_region_explanation). In the same file you can also see what countries go into 
		what region. There is also a country that equals to global, which is for the world (my 
		interpretation; all countries together). That column can be used to see if a specific region or 
		country deviates a lot from what the rest of the world thinks. 

	New shape: (3355829, 11)<BR />
	Columns: Position, Track Name, Artist, Streams, URL, Date, Year, Month, Day, Country, Region<BR /> 
	(the order of the columns also was changed)


## Jupyter Notebook 2 - cleaning_lyrics
Status: in progress

This notebook include: 
- Loading the data
- Looking at the data
- Initial munging and EDA<BR /> 



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
