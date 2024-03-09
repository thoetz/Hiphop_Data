
## Top 10 Most Popular Hip-hop Artists

Here are the hip-hop artists with the highest average popularity scores across all their tracks, making them the top 10 most popular based on this dataset:

1. **cassö**: Average Popularity Score of 92.00
2. **Trueno**: Average Popularity Score of 89.00
3. **David Guetta**: Average Popularity Score of 87.00
4. **Travis Scott**: Average Popularity Score of 87.00
5. **¥$**: Average Popularity Score of 86.09
6. **Post Malone**: Average Popularity Score of 85.22
7. **Anuel AA**: Average Popularity Score of 85.00
8. **Kendrick Lamar**: Average Popularity Score of 84.50
9. **21 Savage**: Average Popularity Score of 84.18
10. **Dua Lipa**: Average Popularity Score of 84.00

```R
SELECT Artist, AVG(Popularity) AS average_popularity
FROM tracks
GROUP BY Artist
ORDER BY average_popularity DESC
LIMIT 10;
```

Now, let's move on to the second analysis: **Longest and Shortest Hip-hop Tracks** in terms of duration.

## Longest and Shortest Hip-hop Tracks

- **Longest Track:**
  - **Artist:** DJ Khaled
  - **Track Name:** GOD DID (feat. Rick Ross, Lil Wayne, Jay-Z, John Legend & Fridayy)
  - **Duration:** 501,648 milliseconds (approximately 8 minutes and 22 seconds)
  - **Track ID:** 2sOj9vyd6yiss9W1IK6chU

- **Shortest Track:**
  - **Artist:** Justin Timberlake
  - **Track Name:** BroZone's Back
  - **Duration:** 81,666 milliseconds (approximately 1 minute and 22 seconds)
  - **Track ID:** 02xkg0KUfiytfbnwAevy1p

```sql
-- Longest track
SELECT Artist, `Track Name`, `Duration (ms)`, `Track ID`
FROM tracks
ORDER BY `Duration (ms)` DESC
LIMIT 1;

-- shortest track
SELECT Artist, `Track Name`, `Duration (ms)`, `Track ID`
FROM tracks
ORDER BY `Duration (ms)`
LIMIT 1;
```

Next, we'll explore the **Distribution of Track Durations** to identify any common patterns or outliers.

## Distribution of Track Durations

![Track Duration Distribution](https://github.com/thoetz/Hiphop_Data/blob/main/track_distribution.png)

```R
library(readr)
tracks <- read_csv("/cloud/project/top_hiphop_artists_tracks.csv")

library(ggplot2)

# Access data from our dataframe named tracks
# Convert duration from milliseconds to minutes
tracks$Duration_min <- tracks$`Duration (ms)` / 60000

# Plot the distribution of track durations
ggplot(tracks, aes(x = Duration_min)) +
  geom_histogram(binwidth = 0.5, fill = "#b9dca8", color = "black") +
  theme_minimal() +
  labs(title = "Distribution of Track Durations",
       x = "Duration (Minutes)",
       y = "Frequency") +
  theme(text = element_text(size = 12))
```

The histogram above shows the distribution of track durations in minutes. We can observe that:

- Most tracks tend to be around 3 to 4 minutes long, which aligns with the typical length of commercial music tracks.
- There's a noticeable skew towards shorter durations, with a long tail extending towards longer tracks. This indicates that while most tracks are within a "normal" range, there are a few tracks that are significantly longer.
- The distribution peaks around the 3 to 4-minute mark, suggesting this is the most common duration for hip-hop tracks in this dataset.

Now, let's move on to the analysis of **Collaboration Patterns Among Top Artists** to see which artists have collaborated the most frequently.

## Collaboration Patterns Among Top Artists

Here are the artists who have collaborated the most frequently, indicating a tendency towards working with other artists or being featured on tracks:

1. **Drake**: 17 collaborations
2. **Eminem**: 11 collaborations
3. **¥$**: 10 collaborations
4. **21 Savage**: 10 collaborations
5. **Timbaland**: 10 collaborations
6. **Ludacris**: 10 collaborations
7. **Lil Nas X**: 10 collaborations
8. **JAY-Z**: 10 collaborations
9. **Flo Rida**: 10 collaborations
10. **Travis Scott**: 9 collaborations

```sql
SELECT Artist, COUNT(*) AS collaborations
FROM tracks
GROUP BY Artist
ORDER BY collaborations DESC
LIMIT 10;
```

This analysis showcases artists who are highly collaborative within the hip-hop genre, potentially indicating clusters or groups of artists who tend to work together frequently.

Finally, let's examine the **Correlation Between Track Duration and Popularity** to see if there's any relationship between how long a track is and how popular it is.

## Correlation Between Track Duration and Popularity

```sql
SELECT CORR(`Duration (ms)`, Popularity)
FROM tracks;
```

The correlation coefficient between **Track Duration** (in milliseconds) and **Popularity** is approximately **0.041**. This value indicates a very weak positive correlation between the duration of a track and its popularity score. Essentially, this suggests that the length of a track has little to no effect on how popular it will be within this dataset.

This analysis helps us understand that factors other than duration are likely more influential in determining a track's popularity in the hip-hop genre.
```
