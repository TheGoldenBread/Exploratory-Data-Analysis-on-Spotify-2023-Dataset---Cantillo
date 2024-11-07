<a name="top"></a>
<p align="center">
<img src="https://github.com/user-attachments/assets/9be4c329-e2f3-40e9-86df-bce547ba8d78" width="200" class="center"> <br>
</p>

<h1 align="center"> :musical_note: An Exploratory Data Analysis on the Spotify 2023 Dataset :musical_note: </h1><br>

### Overview :mag_right:
This project aims to perform an exploratory data analysis (EDA) on Spotify's most streamed songs of 2023.
### Dataset Information :bar_chart:
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
 
<br><hr>
[:top: Back to top](#top)
