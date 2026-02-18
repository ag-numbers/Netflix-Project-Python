# Exploratory Data Analysis project focused on content duration trends
**Business Problem**
Streaming platforms need to understand historical content trends to optimize acquisition strategy.This project analyzes 1990s movie duration patterns to identify potential content gaps

**Key Findings**
	•	The most common movie duration was 100 minutes
	•	Only 7 action movies were shorter than 90 minutes
	•	The duration distribution is right-skewed

**Business Insight**
Short action movies were relatively rare in the 1990s dataset.
If modern audiences show preference for shorter content, this may represent an acquisition opportunity.


#Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

#Read in the Netflix CSV as a DataFrame
netflix_df = pd.read_csv("netflix_data.csv")

#Find most frequent movie duration in 1990s
#Filter for movies
movies= netflix_df[netflix_df['type'] == 'Movie']

#Filter for movies released in the 1990s (1990-1999)
movies_90s = movies[
    (movies['release_year'] >= 1990) &
    (movies['release_year'] <= 1999)
]

#Visualize the duration column in a histogram to see the distribution of movie durations
plt.hist(movies_90s['duration'])
plt.title ('Distribution of movie durations in the 1990s')
plt.xlabel('Duration in min')
plt.ylabel('Number of movies')
plt.show()

#Find the most frequent value
duration= movies_90s['duration'].mode()[0]

#Filter the data again to keep only the Action movies
action_movies_90s= movies_90s[movies_90s['genre']=='Action']

#Start counter
short_movie_count=0

#Now use loops to calculate number of action moviews shorter than 90 min
for label, row in action_movies_90s.iterrows():
    if row ['duration'] <90:
            short_movie_count=short_movie_count+1
    else: 
            short_movie_count=short_movie_count

print(short_movie_count)

#A quicker way of counting values in a column would be to use .sum() on 'duration' but for this specific project, I wanted to showcase the loop function
(action_movies_90s["duration"] < 90).sum()


<img width="620" height="452" alt="Screenshot 2026-02-15 at 17 35 16" src="https://github.com/user-attachments/assets/b2bd4d7d-2384-42d4-8f74-8c52cc72fc1f" />
<img width="366" height="428" alt="Screenshot 2026-02-15 at 17 35 31" src="https://github.com/user-attachments/assets/cb86086e-5f2e-4ade-9829-f6389fbb958c" />
