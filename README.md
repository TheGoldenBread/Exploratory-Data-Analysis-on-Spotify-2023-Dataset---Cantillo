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
- Track Name: Name of the song
- Artist(s) Name: Name of the artist
- Artist(s) Count: Amount of artists who worked on the song
- Streams: Total number of streams on Spotify
- Released Year: The year it was released
- Released Month: The month it was released
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
<p align="justify"> Overall, the dataset contains 953 entries/rows and 24 columns. I was able to find this using. </p>

``` python
df.info()
df.describe()
```
Through this, I was also able to find its data types and those that had missing values, namely;
- In Shazam Charts, with only 903 entries
- Key, with only 858 entries
<p align="justify"> A problem I encountered while trying to interpret the data for <i>Streams</i> was that it was not a correct data type for pandas to interpret as it was classified as an object. So, I enlisted the help of ChatGPT to give me a solution and do something for the missing values.  </p>

``` python
columns_to_convert = ['streams']
df[columns_to_convert] = df[columns_to_convert].apply(pd.to_numeric, errors='coerce')
```
<p align="justify"> Thanks to this code, <i>Streams</i> is now in float64 by converting its invalid entries as NaN and is now able to be interpreted. </p>

<p align="justify">I was given a set of questions that I had to answer, so here are them now.</p>

### Basic Descriptive Statistics :chart_with_upwards_trend:

- What are the mean, median, and standard deviation of the streams column?
  - The values that I got were: <br>
Mean: 514137424.93907565 <br>
Median: 290530915.0 <br>
Standard Deviation: 566856949.0388832
- What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?
<p align="justify">For this I plotted out the released_year and artist_count.</p>
<img src="https://github.com/user-attachments/assets/fb1eaccb-0d9b-4874-b351-695d4caf3eb6" class="center"> <br>
<img src="https://github.com/user-attachments/assets/1c038a5f-8fb4-49e0-8645-f9465fb58cc6" class="center"> <br>
<p align="justify"> As we can see from the graph, the most popular songs are from 2010 onwards. However, there are outliers in which songs date back to the 1900s to the 2000s. For the amount of artists, there are at most 8 artists on a song, which is insane to think about since you'd normally think that 1-2 people would work on a song, 3 is still acceptable, but any amount beyond that is unreal especially 8. </p>

### Top Performers :studio_microphone:
- Which track has the highest number of streams? Display the top 5 most streamed tracks.
<p align="justify"> Using this code, I was able to find the songs with the highest number of streams</p>

``` python
highest_streams = df.sort_values(by='streams', ascending=False).head(5)
highest_streams[['track_name', 'streams']]
```
<p align="justify">Which were:</p>

1. Blinding Lights with 3.7 billion streams
2. Shape of You with 3.5 billion streams
3. Someone You Loved with 2.8 billion streams
4. Dance Monkey with 2.8 billion streams
5. Sunflower - Spider-Man: Into the Spider-Verse with 2.8 billion streams <br>

- Who are the top 5 most frequent artists based on the number of tracks in the dataset?

``` python
top_artists = df['artist(s)_name'].value_counts().head(5)
top_artists
```
<p align="justify"> With this, I was able to find the most frequent artists who appeared.</p>

1. Taylor Swift appeared with a staggering amount of 34 times
2. The Weeknd appeared 22 times
3. Bad Bunny appeared 19 times
4. SZA appeared 19 times
5. Harry Styles appeared 17 times

## Temporal Trends :chart_with_downwards_trend:
- Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.
``` python
tracks_per_year = df['released_year'].value_counts().sort_index()
```
<p> Using that, I was able to group up the released_year and count the number of tracks that was released each year. Then from that using matplotlib, I was able graph that group. </p>
<img src="https://github.com/user-attachments/assets/9eaaaf82-6fa0-4d42-ac34-c7e4599b8787" class="center"> <br>

<p align="justify"> We can see from the graph that there is a steady release rate of songs from the 1930s to the 2000s, with some minor fluctuations in some years always below 50 tracks per year. Then there is a gradual increase starting from the year 2000, then a massive spike around the year 2020, which is the time when the pandemic happened, which leads me to believe that the spike was caused by people quarantined at their homes, leading to a widespread use of media. </p>

- Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?
<p align="justify"> Same thing done to previous question, group the released_month and plot that. However, the values for the months were in 1-12 but I wanted them to be in names so I asked ChatGPT for some help and managed to do it.</p>
<img src="https://github.com/user-attachments/assets/92162bd1-c2fb-4452-a001-996430269a30" class="center"> <br>
<p align="justify"> From the graph, we can see that there are some noticeable patterns, especially in January, where it experiences the most track releases, and May, the second highest month to release tracks. This suggests that there are some preferences for releasing in this  year. After May, it experiences a dip up to August, then it increases again up to November. These could be influenced due to some marketing strategies, holiday seasons, or some consumer behavior in the works.</p>

## Genre and Music Characteristics

- Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?
<p align="justify"> For this I had to make a correlation matrix between the needed variables. Then I'd have to plot that into a heatmap to see its correlation with each other. </p>

```python
correlation_matrix = df[['streams', 'bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%']].corr()
```
<p align="justify"> Using that I was able to get its correlation matrix. All I need is to graph it. </p>
<img src="https://github.com/user-attachments/assets/511cc0e9-382f-412f-acb9-93ede4b4789e" class="center"> <br>
<p align="justify"> According to the heatmap, it seems like there is no significant correlation between streams and their musical attributes due to its value being in the negatives and close to zero. This suggests that the popularity of the tracks may be affected by some other factors. </p>

- Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?
<p align="justify"> Going back to the heatmap again, the value of the correlation between danceability and energy is 0.2, which is a low positive correlation; this implies that there is a tendency for high-energy tracks to be danceable. For the relationship between valence and acousticness, the correlation between them is -0.082, which means that a track that is acoustic has nothing to do with its valence or its positivity.  </p>

## Platform Popularity
- How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?


<br><hr>
[:top: Back to top](#top)
