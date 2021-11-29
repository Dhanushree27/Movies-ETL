# Extract, Transform and Load of Movies dataset

## Overview
This project was undertaken to create a clean dataset of movies with their ratings for a hackathon to develop an algorithm to identify which low budget movies will become popular. This was achieved using ETL process

### Extraction
The data was extracted from two sources:
a. Wikipedia- json file with a list of movies, containing 193 columns and 7311 records
b. Kaggle-Movie data as csv file, containing 24 columns and 45467 records
c. Kaggle-Rating data from MovieLens as csv file, containing 4 columns and 26,024,289 records 
Wikipedia data was used as base for list of movies to consider. All three files were transformed to remove duplicates, format columns, remove unncessary columns and other transformations.

### Transformation
Wikipedia data:
a. Filtered out movies that don't have a IMDB link and a Director ('Directed By','Director')
b. Filtered out TV shows based on no. of episodes 
c. Grouped alternate language titles into a single column Alternate titles, via a function
d. Combined duplicate columns into single column, via a function
e. Removed duplicate rows based on imdb id (Created using regex exp)
f. Removed columns that don't have even 10% data
g. Formatted the data so that they have same pattern or type (box office, budget, release date, running time) 
h. Converted data to proper numeric or datetime format

Kaggle Movie data:
a. Drop adult movies
b. Convert data to proper numeric or datetime format

Merge and Transform:
The two datasets were then merged on IMDB ID. The resulting mismatched columns were then analysed and decision was made to drop Wikipedia columns. In cases where there was missing data in Kaggle columns, data was copied from Wikipedia columnn and then the columns were dropped, using a function.

Reorder and Rename:
The columns in the final movies dataframe were then reordered and renamed for convenience

Ratings data:
a. Grouped by movie ID and rating to obtain count for each rating.
b. Merged rating count data with the movies dataframe to obtain a movies and ratings dataframe 
c. Replaced ratings with null values with 0

### Load
The movies dataframe and the ratings file were loaded into database.
Movies dataset: The final cleaned data contained 31 columns and 6052 records
Ratings dataset: Loaded in chunks since file was a large file with 26,024,289 records
