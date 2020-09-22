# Spotify-Playlist-Analysis-with-Python-and-Spotipy
Using Python and Spotify's API, I created an analysis/comparison of my favorite English songs and Chinese songs. I wanted to compare a set of my favorite English songs and Chinese songs because due to COVID-19, I've been staying in Taipei this semester (instead of Los Angeles, where I go to school), which has gotten me to start listening to more songs in Chinese. I thought it would be fun to do an analysis of these Chinese songs I've started listening to and compare it to the English songs I like.

## Goal
To see if my taste in music is similar in different languages, and to get to know my music taste a little better through numbers and visualizations.

## [Data Collection, Feature Engineering, Data Preprocessing](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/authorization_extractfeatures.ipynb)

### Data Collection + Extracting Music and Audio Features
I used [Spotipy](https://spotipy.readthedocs.io/en/2.13.0/), a lightweight Python library for the Spotify Web API. With Spotipy, I get full access to all of the music data provided by the Spotify platform. 

I looked at [makispl's repository](https://github.com/makispl/Spotify-Data-Analysis) to help write the Authorization Flow code to gain access to Spotify's data.

I was also inspired by [jmcabreira's repo](https://github.com/jmcabreira) for this project.

Once the authorization to my Spotify profile was granted, I continued to follow along with parts of makispl's repository and created functions to extract a user's playlist, a user's playlists' tracks, and a track's audio feature. I extracted audio features for songs in two of my playlist (favorite English songs and favorite Chinese songs).

These are the features extracted and their definition (taken from the Spotify documentation linked above):
 - Acousticness : A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic.
- Danceability : Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable.
- Energy : Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale. Perceptual features contributing to this attribute include dynamic range, perceived loudness, timbre, onset rate, and general entropy.
- Instrumentalness: Predicts whether a track contains no vocals. “Ooh” and “aah” sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly “vocal”. The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0.
- Liveness: Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live.
- Loudness: he overall loudness of a track in decibels (dB). Loudness values are averaged across the entire track and are useful for comparing relative loudness of tracks. Loudness is the quality of a sound that is the primary psychological correlate of physical strength (amplitude). Values typical range between -60 and 0 db.
- Speechiness: Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks.
- Valence: A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry).
- Tempo: The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration.

### Data Preprocessing + Feature Engineering
Since I have more tracks in my English song playlist, I randomly selected 37 songs to match the size of my Chinese song playlist. I have fewer songs in the Chinese playlist because I don't know as many songs in Chinese compared to songs in English. 

I dropped unnecessary features such as 'track_name' beacuse I wouldn't need to know the name of the song in the analysis, I will only be using audio features. I also creaded a 'track_id' column.

### Normalization of Features
I had to normalize the features so they contained values ranging from 0 to 1 because two of the features, tempo and loudness, were on a much higher scale than the others, which would make analysis (especially visualizing) difficult.

### Saved as CSV
I then saved the audio feature data for the 2 different playlists into 2 separate CSV files which I will read from for the [analysis of the music](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/Analysis%20Chinese%20vs%20English.ipynb).

This is what the resulting data looks like:
![result_data](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/pics/data.png)

## [Data Analysis](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/Analysis%20Chinese%20vs%20English.ipynb)
Based on my own view on my music taste and favorite genres (slow pop, ballads, sad songs), I hypothesized that my music taste would be similar even in different languages, and that they would be:
- lower in valence (musical positiveness)
- lower in tempo (speed)
- lower in loudness
- lower in energy
- higher in speechiness

Here are some of my analysis and visualizations I created:

I used Spotify's green and black colors for visualization :)

### 1. Audio Feature Distributions with Histograms
![histograms](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/pics/histograms.png)

### 2. Heatmaps of Correlation Among Audio Features
![correlations](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/pics/correlations.png)

### 3. Mean Values of Audio Features on a Bar Chart
![bar](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/pics/bar.png)

### 4. I also created metrics for determining how diversified my playlists are using the average of the standard deviations of each audio feature.
![variety](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/pics/variety.png)

## Conclusion
From many of the graphs, especially the one about the averages of the audio features, it can be inferred that the two playlists are pretty similar. Their means were relatively close to each other and the from the histogram, it can be seen that the spreads of the audio features were pretty similar when comparing the English and Chinese Songs.

I was correct in that many of my songs weren't high in valence nor tempo because valence measures the positivity of a song, and I like to listen to slower and sadder music. However, the levels of some of the audio features surprised me. I thought my music would be loud and less speechy. Loudness ended up as the feature with the highest mean for both playlists and speechiness had the lowest means. This could be explained by loudness and speechiness both don't necessarily have a very strong correlation with valence as shown on the heat maps (and I based my assumptions on low valence). The correlation of those two features with valence are very low especially for the English songs (<0.08).

Turns out, I think I was right in that my music taste isn't super diversified beacuse when I calculated the average of the standard deviations of my songs' audio feature, it came out to be around 0.22 which I think is pretty low. It was this amount for both the English and Chinese playlists.

## Next Steps
Next time, I would want to try to look at a bigger subset of my music becuase this time I only had 37 songs from each playlist (since I don't listen to as many Chinese songs). Moving forward, I will also try to apply machine learning in my analysis -- perhaps in predicting which playlists a song belongs in or make song recommendations based on playlist of songs.
