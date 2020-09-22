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

### Normalize features
I had to normalize the features so they contained values ranging from 0 to 1 because two of the features, tempo and loudness, were on a much higher scale than the others, which would make analysis (especially visualizing) difficult.

### Saved into CSV
I then saved the audio feature data for the 2 different playlists into 2 separate CSV files which I will read from for the [analysis of the music](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/Analysis%20Chinese%20vs%20English.ipynb).

## [Data Analysis](https://github.com/justinezth/Spotify-Playlist-Analysis-with-Python-and-Spotipy/blob/master/Analysis%20Chinese%20vs%20English.ipynb)


## Conclusion

## Next Steps
