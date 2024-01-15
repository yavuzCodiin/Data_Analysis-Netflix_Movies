# <ins>Data_Analysis-Netflix_Movies</ins>
This project is about understanding Netflix movies better using pandas and matplotlib. It's all about finding interesting patterns and details in the movie dataset.

## <ins>Importing libraries and Loading the CSV file</ins>
```python
import pandas as pd
import matplotlib.pyplot as plt

netflix_df = pd.read_csv("netflix_data.csv")
```

![image](https://github.com/yavuzCodiin/Data_Analysis-Netflix_Movies/assets/82445309/c689a5f5-d330-4b55-a308-34138f0fee36)

## <ins>Filtering the data to remove TV shows and store as netflix_subset</ins>
```python
netflix_subset = netflix_df[netflix_df["type"] == "Movie"]
```

![image](https://github.com/yavuzCodiin/Data_Analysis-Netflix_Movies/assets/82445309/99371d6a-3ab4-4e0c-9637-b2169eb3f146)

## <ins>Investigating the Netflix movie data, and keeping only the columns "title", "country", "genre", "release_year", "duration", and saving this into a new DataFrame called netflix_movies</ins>
```python
netflix_movies = netflix_subset[["title", "country", "genre", "release_year", "duration"]]
```

![image](https://github.com/yavuzCodiin/Data_Analysis-Netflix_Movies/assets/82445309/4ebf3e95-7846-49ef-96e1-db9089b881f5)

## <ins>Filtering netflix_movies to find the movies that are shorter than 60 minutes, and  saving the resulting DataFrame as short_movies</ins>
```python
short_movies = netflix_movies[netflix_movies.duration < 60]
```

![image](https://github.com/yavuzCodiin/Data_Analysis-Netflix_Movies/assets/82445309/22dfd251-b08c-4d6e-8f2a-ed93022f1748)

## <ins>Inspecting for possible contributing factors</ins>
```python
short_movies["genre"].value_counts() #most of them are Children movies, Documentaries, Stand-Ups
```

![image](https://github.com/yavuzCodiin/Data_Analysis-Netflix_Movies/assets/82445309/66460b05-48dc-4932-bfd5-15519449db9a)

```python
short_movies["duration"].sum() #17633 minutes of content under 60 minutes
```

```python
short_movies["country"].value_counts() # most of them are from US, UK, CA rest is almost same
```

![image](https://github.com/yavuzCodiin/Data_Analysis-Netflix_Movies/assets/82445309/882cbcf3-55c1-48bb-a260-a6e31e38a320)

## <ins>Configuration for color assignment for scatter plot</ins>
```python
genre_colors = {
    "Children": "red",
    "Documentaries": "blue",
    "Stand-Up": "green"
}

# Loop over the genre-color pairs
for genre, color in genre_colors.items():
    # Filter movies by genre
    genre_movies = netflix_movies[netflix_movies.genre == genre]
    # Plot each genre with its respective color
    plt.scatter(genre_movies.release_year, genre_movies.duration, color=color, label=genre)

# Plot remaining genres as 'Other'
other_movies = netflix_movies[~netflix_movies.genre.isin(genre_colors.keys())]
plt.scatter(other_movies.release_year, other_movies.duration, color="black", label="Other")
```

## <ins>Creating figure and configuration for plot</ins>
```python
fig = plt.figure(figsize=(12,8))

# Create a title and axis labels
plt.title("Movie Duration by Year of Release")
plt.xlabel("Release year")
plt.ylabel("Duration (min)")

# Show the legend
plt.legend()

# Show the plot
plt.show()

```
![image](https://github.com/yavuzCodiin/Data_Analysis-Netflix_Movies/assets/82445309/0cb7581d-4b12-4b44-bbba-c2edc7d8079d)


