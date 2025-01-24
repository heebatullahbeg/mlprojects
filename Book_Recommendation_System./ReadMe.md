# Project Overview

An ML-powered book recommendation system using content-based filtering with TF-IDF vectorization and cosine similarity.
This readme file is a project overview of **content_based_book_recommendation_system_V1**

### Dataset
This data was collected in an attempt to personally identify more books that one would like based on ones they may have read in the past.
It comprises some (around 10k) of the most recommended books of all time.
(link: https://www.kaggle.com/datasets/ishikajohari/best-books-10k-multi-genre-data)

### Features

1. **Book** - Name of the book.
2. **Author** - Name of the book's Author
3. **Description** - The book's description, as mentioned on Goodreads
4. **Genres** - Multiple Genres as classified on Goodreads
5. **Average Rating**- The average rating (Out of 5) given on Goodreads
6. **Number of Ratings** - The Number of users with Ratings. (Not to be confused with reviews)
7. **URL** - The Goodreads URL for the book's details page

## **Data Pipeline**
### **Data Loading**
Load the dataset (goodreads_data.csv) containing information about books with the following features:

### **Data Cleaning**
Handles missing values by replacing NaNs with empty strings in selected features (Description, Genres, and Author).

### **Feature Engineering**
Combine Description, Genres, and Author into a single textual feature, books_data_features, to provide a rich context for recommendations.

### **Vectorization**
Use TfidfVectorizer to convert the combined textual data into a numerical feature vector.

### **Similarity Computation**
Compute pairwise cosine similarity between all book feature vectors to create a similarity matrix.

## Recommendation Logic
1. Allow users to input their favorite book title.
2. Find the closest matching title.
3. Retrieve similar books from the precomputed cosine similarity matrix.
4. Recommend the top 30 similar books and display their titles.

### Output

![image](https://github.com/user-attachments/assets/3a16f9a6-c66a-47b6-b506-cff3adc78271)
