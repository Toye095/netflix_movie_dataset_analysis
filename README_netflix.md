# Project: Netflix Movie Dataset Analysis and Visualization

## Table of Contents
* 1. Overview
* 2. Dataset Description
* 3. Project Files
* 4. Project Workflow
    * a. Data Preparation
    * b. Data Cleaning
    * c. Data Exploration
    * d. Data Visualization
    * e. R integration
* 5.Key Insights
* 6. Requirements
* 7. Usage

## 1. Overview
Netflix is a digital movie subscription platform and the objective of this project is to derive insights from Netflix shows and movies, focusing on their genres, ratings, and other key attributes. This repository contains a jupiter notebook to read a zipped netflix_data csv file and perform cleaning, exploration, and visualization exercises. An R script is also provided to visualize the movies rating distribution.

## 2. Dataset Description
The dataset contains details of Netflix movies and TV shows. Key columns include:

* `Type`: Movie or TV Show
* `Title`: Name of the content
* `Director`: Director of the content
* `Cast`: Key actors
* `Country`: Country of origin
* `Date Added`: When the content was added to Netflix
* `Rating`: Age rating of the content
* `Duration`: Duration of the movie or number of seasons for TV shows
* `Genres`: Categories the content belongs to (e.g., Drama, Comedy)

## 3. Project Files
* Netflix_Visualization_Toye.ipynb 
* Netflix_Visualization_Toye_R.R 
* README_netflix.md - Documentation.

## 4. Project Workflow
1. **Data Preparation**: 
   - unzip dataset, rename folder, check few rows, check dataset dimension, analyse data type and check missing values.
CODE:
  with zipfile.ZipFile('NetflixData.zip', 'r') as zip_ref:
    zip_ref.extractall('Netflix_Data')
os.rename('Netflix_Data', 'Netflix_shows_movies_')
nd = pd.read_csv('Netflix_shows_movies_/netflix_data.csv')
nd.head()
print('The netflix dataset has {} Rows and {} Columns'.format(nd.shape[0], nd.shape[1]))
nd.info()
nd.isnull().sum()

========================================================================================

2. **Data Cleaning**: 
   - Create custom function to fill missing values, apply function and confirm missing values were treated.

CODE:
nd.isna().sum()

=========================================================================================

3. **Data Exploration**: 
   - Statistical summary of dataset, statistical analysis of values and distribution.

CODE:
nd.describe().T
nd.describe(include='object').T
print("Unique ratings:\n", nd['rating'].value_counts()) # distribution of ratings

type_counts = nd['type'].value_counts()        # content type
print("\nType distribution:\n", type_counts)

==========================================================================================

4. **Data Visualization**: 
   - Visualize key patterns and distributions.
   
 CODE:
* Top 10 Most Watched Genres 
plt.figure(figsize=(10, 6))
genre_counts = nd['listed_in'].str.split(', ').explode().value_counts().head(10)
sns.barplot(x=genre_counts.values, y=genre_counts.index, palette='viridis')
plt.title("Top 10 Most Watched Genres")
plt.xlabel("Number of Shows/Movies")
plt.ylabel("Genre")
plt.show()

* Ratings Distribution
plt.figure(figsize=(8, 5))
sns.countplot(data=nd, x='rating', order=nd['rating'].value_counts().index, palette='viridis')
plt.title("Ratings Distribution")
plt.xlabel("Rating")
plt.ylabel("Count")
plt.xticks(rotation=45)
plt.show()

=============================================================================================

5. **R Integration**: 
   - Implement rating distribution in R.

CODE:
library(ggplot2)

* Read the CSV file
netflix_data <- read.csv("C:/Users/Dell/Downloads/netflix_data.csv")

* Create a bar plot for ratings distribution
ggplot(netflix_data, aes(x=rating)) +
  geom_bar() +
  labs(title="Ratings Distribution", x="Rating", y="Count") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
  
===============================================================================================  

## 5. Key Insights
* Dataset Composition:
    * Twice as many movies as TV shows.
    * Most content is listed as Documentaries, Dramas, and Comedies.
 * Ratings Analysis:
    * The most common rating is TV-MA.
    * The least common rating is NC-17.
* Movies:
    * The average duration of a Netflix movie is approximately 90 minutes.


## 6. Requirements
* Python 3.8+
* Libraries:
    * pandas
    * matplotlib
    * seaborn
    * zipfile
    * os
* R Studio
* Library: ggplot2

## 7. Usage

* Clone the repository or download zipped file.
* Ensure the dataset (NetflixData.zip) is placed in the working directory.
* Run python notebook and R script
* Review the output for insights and visualizations



```python

```
