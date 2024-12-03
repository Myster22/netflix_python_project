# Data Analysis of Netflix content using Python
![Netflix logo](https://github.com/Myster22/netflix_python_project/blob/main/logo.png)
## Objective
- Analyze the different types of content
- Compare the types of  content
- Identify the most common ratings for movies and TV shows.
- Analyze the distribution of content by country
- Analyze the popular genre
- Analyze the top cast for a specific country
- Analyze the top directors
- Analyze the release patterns
## Dataset
The data for this project is sourced from the Kaggle dataset:
- Dataset link : [Netflix Data](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)
## Business Problems and Solutions
### 1. Different types of content
```python
    df["type"].unique()
```
### 2. Compare the types of  content
```python
    count = df["type"].value_counts()
```
### 3. Identifying the most common ratings for movies and TV shows
```python
    most_common_rating = df.groupby('type')['rating'].agg(lambda x: x.mode()[0]).reset_index()
```
### 4. Analyzing the distribution of content by country
```python
    df_cleaned = df.dropna(subset=['country']).copy()  # Remove rows where country is Null or missing values
    df_cleaned['country'] = df_cleaned['country'].str.split(',')
    df_exploded = df_cleaned.explode('country')
    country_counts = df_exploded['country'].value_counts()
    top_5_countries = country_counts.head(5)
```
### 5. Analyzing the popular genre
```python
    df_clean = df.dropna(subset=['listed_in']).copy()  # Remove rows where listed_in is Null or missing values
    df_clean['listed_in'] = df_clean['listed_in'].str.split(',')
    df_explode = df_clean.explode('listed_in')
    genre_counts = df_explode['listed_in'].value_counts()
    top_5_genre = genre_counts.head(5)
```
### 6. Analyzing the top cast for a specific country
```python
    df_clean = df.dropna(subset=['country', 'cast']).copy()
    df_clean['country_clean'] = df_clean['country'].apply(lambda x: [country.strip() for country in str(x).split(',')])
    df_clean = df_clean.explode('country_clean')
    india_data = df_clean[df_clean['country_clean'] == 'India'].copy()
    india_data['cast_clean'] = india_data['cast'].apply(lambda x: [actor.strip() for actor in str(x).split(',')])
    india_data = india_data.explode('cast_clean')
    top_cast = india_data['cast_clean'].value_counts().head(10)
```
### 7. Analyzing the top directors
```python
    df_clean = df.dropna(subset=['director']).copy()
    df_clean['director'] = df_clean['director'].apply(lambda x: [country.strip() for country in str(x).split(',')])
    df_clean = df_clean.explode('director')
    top_directors = df_clean['director'].dropna().value_counts().reset_index()
    top_directors.columns = ['Director', 'Content Count']
    display(top_directors.head(5))
```
### 8. Analyzing the release patterns 
```python
    release_year_counts = df_clean['release_year'].value_counts().sort_index()
    movies = df_clean[df_clean['type'] == 'Movie']
    tv_shows = df_clean[df_clean['type'] == 'TV Show']
    movies_by_year = movies['release_year'].value_counts().sort_index()
    tv_shows_by_year = tv_shows['release_year'].value_counts().sort_index()
```
## Findings and Conclusion
- **Content Distribution**: The dataset contains a diverse range of movies and TV shows with varying ratings and genres.
- **Common Ratings**: Insights into the most common ratings provide an understanding of the content's target audience.
- **Geographical Insights**: This insights help us to know where people are watching more of the contents and retain and grow the base                                of audience.
- **Top Casts**: Like in our analysis we chose India to filter out top cast in India.So, we can collaborate with this cast and market 
                 our content and website to grow our customer base.
- **Top Directors**: This insights will help us to improve our content by collaborating with best directors.
- **Release Patterns**: By This insights we can know seasonal trends ,binge Watching Trends and balance between Movies and TV Shows.
## Recommendations
- Partner with high-performing regions and talents.
- Create content in popular genres with a focus on popular casts.
- Focus on modern, region-specific, and contents which connects with people.

    

