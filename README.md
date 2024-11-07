<a name="top"></a>
<p align="center">
<img src="https://github.com/user-attachments/assets/9be4c329-e2f3-40e9-86df-bce547ba8d78" width="200" class="center"> <br>
</p>

<h1 align="center"> :musical_note: An Exploratory Data Analysis on the Spotify 2023 Dataset :musical_note: </h1><br>

### Overview :mag_right:
This project aims to perform an exploratory data analysis (EDA) on Spotify's most streamed songs of 2023.
### Dataset Information :bar_chart:
The data was taken from https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023 <br>
This dataset contains various features of popular Spotify songs; however, only necessary ones will be focused on, such as its <br>
- Streams: Total number of streams on Spotify
- Released Year: The year it was released
- Released Month: The month it was released
- Released Day: The day of the month when it was released
- BPM: Beats per minute
- Key: Key of the song
- Mode: Mode of the song (major or minor)
- Danceability %: Percentage indicating how suitable the song is for dancing
- Valence %: Positivity of the song's musical content
- Energy %: Perceived energy level of the song
- Acousticness %: Amount of acoustic sound in the song
- Instrumentalness %: Amount of instrumental content in the song
- Liveness %: Presence of live performance elements
- Speechiness %: Amount of spoken words in the song
<br><br>
<p> Overall, the dataset contains 953 entries/rows and 24 columns I was able to find this through. </p>

``` python
df.info()
df.describe()
```
Through this, I was also able to find its data types and those that had missing values, namely;
- In Shazam Charts, with only 903 entries
- Key, with only 858 entries
<p> A problem I encountered while trying to interpret the data for <i>Streams</i> was that it was not a correct data type for pandas to interpret as it was classified as an object. So, I enlisted the help of ChatGPT to give me a solution and do something for the missing values.  </p>

``` python
columns_to_convert = ['streams']
df[columns_to_convert] = df[columns_to_convert].apply(pd.to_numeric, errors='coerce')
```
<p> Thanks to this code <i>Streams</i> is now in float64 by converting its invalid entries as NaN and is now able to be intepreted. </p>

### Basic Descriptive Statistics :chart_with_upwards_trend:
<p>I was given a set of questions that I had to answer so here are them now.</p>

- What are the mean, median, and standard deviation of the streams column?
  - The values that I got were: <br>
Mean: 514137424.93907565 <br>
Median: 290530915.0 <br>
Standard Deviation: 566856949.0388832
 
<br><hr>
[:top: Back to top](#top)
