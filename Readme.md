# Music Streaming Data Analysis

## Overview
This project analyzes user listening behavior from a music streaming service using Apache Spark. It processes large-scale streaming data to derive meaningful insights, such as users' favorite genres, top songs, and personalized recommendations.

## Tech Stack
- **Apache Spark** (PySpark) for big data processing
- **Pandas** and **NumPy** for dataset generation
- **CSV** files for storing input and output data

## Dataset Generation
Two datasets are created for analysis:
1. **Listening Logs (`listening_logs.csv`)**
   - Simulates user listening behavior with fields: `user_id`, `song_id`, `timestamp`, and `duration_sec`.
2. **Songs Metadata (`songs_metadata.csv`)**
   - Contains song details with fields: `song_id`, `title`, `artist`, `genre`, and `mood`.

## Tasks Implemented
### Task 1: Find Each User's Favorite Genre
- Joins listening logs with song metadata.
- Groups by `user_id` and `genre` to count listens.
- Determines the most frequently listened genre per user.
- **Output:** `output/user_favorite_genres`
### Sample_Output :
user_1,Pop,52
user_10,Rock,5
user_11,Jazz,2
user_12,Classical,2
user_13,Rock,5

### Task 2: Calculate Average Listen Time Per Song
- Groups listening logs by `song_id`.
- Computes the average listen duration for each song.
- **Output:** `output/avg_listen_time_per_song`
### Sample_Output :
song_19,159.8695652173913
song_47,184.57142857142858
song_38,178.47619047619048
song_37,163.42857142857142

### Task 3: List Top 10 Most Played Songs This Week
- Extracts `year` and `week` from timestamps.
- Filters data for the most recent week.
- Counts song plays and selects the top 10.
- **Output:** `output/top_songs_this_week`
### Sample_Output :
song_3,4,Title_3,Artist_3,Classical,Happy
song_33,3,Title_33,Artist_33,Pop,Happy
song_19,2,Title_19,Artist_19,Classical,Sad
song_32,2,Title_32,Artist_32,Jazz,Sad

### Task 4: Recommend "Happy" Songs to Users Who Mostly Listen to "Sad" Songs
- Identifies users whose majority listening history (>50%) is "Sad".
- Finds "Happy" songs they haven't played.
- Recommends up to 3 songs per user.
- **Output:** `output/happy_recommendations`
### Sample_Output :
user_13,song_15,Title_15,Artist_15
user_13,song_16,Title_16,Artist_16
user_13,song_18,Title_18,Artist_18
user_2,song_18,Title_18,Artist_18

### Task 5: Compute Genre Loyalty Score
- Determines the total plays per user.
- Identifies the most played genre per user.
- Calculates loyalty score = (most played genre plays / total plays).
- Filters users with loyalty score > 0.8.
- **Output:** `output/genre_loyalty_scores`
### Sample_Output :
user_39,1,1,1.0
user_1,61,52,0.8524590163934426
user_2,62,52,0.8387096774193549

### Task 6: Identify Night Owl Users
- Extracts the `hour` from timestamps.
- Filters users who stream between 12 AM - 5 AM.
- **Output:** `output/night_owl_users`
### Sample_Output :
user_58
user_94
user_73
user_85
user_14

## Running the Project
1. **Generate the datasets:**
   ```sh
   python generate_data.py
   ```
2. **Run the Spark analysis:**
   ```sh
   spark-submit music_analysis.py
   ```
3. **Check the output in the `output/` directory.**
