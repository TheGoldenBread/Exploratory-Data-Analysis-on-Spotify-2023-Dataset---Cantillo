<a name="top"></a>
<p align="center">
<img src="https://github.com/user-attachments/assets/9be4c329-e2f3-40e9-86df-bce547ba8d78" width="200" class="center"> <br>
</p>

<h1 align="center"> :musical_note: An Exploratory Data Analysis on the Spotify 2023 Dataset :musical_note: </h1><br>

<h4> Table of Contents </h4>

- [Overview](#overview)
- [Dataset Information](#dataset)
- [Basic Descriptive Statistics](#basic)
- [Top Performers](#topp)
- [Temporal Trends](#temporal)
- [Genre and Music Characteristics](#genre)
- [Platform Popularity](#platform)
- [Advanced Analysis](#advanced)

<a name="overview"/>

### Overview :mag_right:
This project aims to perform an exploratory data analysis (EDA) on Spotify's most streamed songs of 2023.

<a name="dataset"/>

### Dataset Information :bar_chart:
The data was taken from https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023 <br>
This dataset contains various features of popular Spotify songs; however, only necessary ones will be focused on, such as its <br>
- Track Name: Name of the song
- Artist(s) Name: Name of the artist
- Artist(s) Count: Amount of artists who worked on the song
- Streams: Total number of streams on Spotify
- Released Year: The year it was released
- Released Month: The month it was released
- In Spotify Playlists: Number of Spotify playlists the song is included in
- In Spotify Charts: Presence and rank of the song on Spotify charts
- BPM: Beats per minute
- Key: Key of the song
- Mode: Mode of the song (major or minor)
- Danceability %: Percentage indicating how suitable the song is for dancing
- Valence %: Positivity of the song's musical content
- Energy %: Perceived energy level of the song
- Acousticness %: Amount of acoustic sound in the song

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

<a name="basic"/>

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

<a name="topp"/>

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

<a name="temporal"/>

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

<a name="genre"/>

## Genre and Music Characteristics :notes:

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

<a name="platform"/>

## Platform Popularity :computer:
- How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?
<p align="justify"> What I did here was take the count and average of the playlist and chart and plotted that. </p>

``` python
playlist_counts = df[["in_spotify_playlists", "in_spotify_charts", "in_apple_playlists"]].sum()
playlist_average = df[["in_spotify_playlists", "in_spotify_charts", "in_apple_playlists"]].mean()
```
<p align="justify"> Using those I was able to get their count and average. Plotting those resulted in these graphs. </p>
<img src="https://github.com/user-attachments/assets/5a6c0355-0fd8-4201-a701-cd19eb09e133" class="center"> <br>
<p align="justify"> We could see that Spotify favors the more popular tracks more than Apple's. </p>

<a name="advanced"/>

## Advanced Analysis :mag:

- Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?
<p align="justify"> I had no clue on what to do here so I just asked ChatGPT straight up. </p>

``` python
streams_pattern_keymode = df.groupby(["key", "mode"])["streams"].agg(["mean", "median"]).reset_index()
```
<p align="justify"> That was the solution that I got which I think takes the mean and median of the streams and groups it based on the key and mode. After that I plotted it. </p>
<img src="https://github.com/user-attachments/assets/ac153972-1c04-45d6-b480-f8f6df574d11" class="center"> <br>
<p align="justify">Tracks in the key of E major have the highest average streams among all keys and modes, which indicates that this key in particular might be popular, or tracks that have a high streaming count mostly use this key. Comparing the major and minor modes, major has the higher average stream count; this suggests that listeners often prefer songs with major keys, which makes sense since those songs are more upbeat. This is probably helpful for producers who want to make a song based on the current trends.</p>

- Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.
<p align="justify"> I had no idea what to do here too. </p>

``` Python
# Sum playlist and chart counts by artist
artist_playlist_counts = df.groupby("artist(s)_name")[["in_spotify_playlists", "in_spotify_charts", "in_apple_playlists"]].sum()

# Sort by total appearances across all platforms
artist_playlist_counts["total_appearances"] = artist_playlist_counts.sum(axis=1)
top_artists = artist_playlist_counts.sort_values("total_appearances", ascending=False).head(10)
print(top_artists)
```
<p align="justify"> Yeah... So here it takes the sum of the playlist and charts and groups that by the artist's names. After it counts the total appearances of each artist on both platforms, sorts them in descending order, and displays the top 10. Ofcourse after that we need to plot it to better visualize it.</p>
<img src="https://github.com/user-attachments/assets/47ed0f3c-6d9d-4e08-9486-e13ae40e037c" class="center"> <br>
<p align="justify"> That's for the total number of appearances on both platforms. </p>
<img src="https://github.com/user-attachments/assets/f2f9c110-5500-4c94-9a4f-8478dd0a99fa" class="center"> <br>
<p align="justify"> That's for the total number of appearances on Spotify playlist. </p>
<img src="https://github.com/user-attachments/assets/fa962b48-07a7-4fca-a6f6-b0c66aed47cb" class="center"> <br>
<p align="justify"> That's for the total number of appearances on Spotify charts. </p>
<img src="https://github.com/user-attachments/assets/f67c4ee5-be41-43ce-be79-a85b6de51173" class="center"> <br>
<p align="justify"> That's for the total number of appearances on Apple playlist. </p>
<p align="justify"> We can see that in terms of Spotify playlists, The Weeknd is number one. This is because this artist is often in songs with 2 or more collaborators adding up to the count. But in Spotify charts, Taylor Swift is number one. Meanwhile, in the Apple playlist, it's a close battle between Taylor Swift, Harry Styles, and The Weeknd.  </p> <br><br>

<p align="justify"> Well uh that's it for this Exploratory Data Analysis. Thank you for going through much of your time in reading this. </p> 

![](https://github.com/user-attachments/assets/fafb8cf7-b092-4adc-9f59-17c8fa58d1eb)


<br><hr>
[:top: Back to top](#top)
