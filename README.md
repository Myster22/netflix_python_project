# Data Analysis of Netflix content
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
    counts_df = count.reset_index()
    counts_df.columns = ['Type', 'Count']
    sns.barplot(x='Type', y='Count', data=counts_df, palette='pastel', hue='Type', dodge=False, legend=False)
    plt.title('Count of Movies and TV Shows')
    plt.xlabel('Type')
    plt.ylabel('Count')
    for index, row in counts_df.iterrows():
    plt.text(index, row['Count'], str(row['Count']), ha='center', va='bottom')
    plt.show()
```
