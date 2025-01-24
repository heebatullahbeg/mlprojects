# 📚 Book Recommendation System with Visualizations
This project provides personalized book recommendations based on user input, leveraging content similarity and machine learning techniques. It also includes meaningful data visualizations to help users better understand book trends and ratings.

## 📂 Dataset
The dataset used in this project contains the following features:

**Book:** Title of the book.
**Author:** Name of the author(s).
**Description:** A brief description of the book.
**Genres:** Genre(s) of the book.
**Avg_Rating:** Average rating of the book on a 5-point scale.
**Num_Ratings:** Total number of ratings received.
**URL:** A link to the book's page for additional details.

## 📊 Visualizations

**Correlation Matrix**
Moderate positive correlation (0.628) between the average ratings and number of book ratings.
This suggests that books with higher ratings tend to have more ratings.


![image](https://github.com/user-attachments/assets/8d9833cd-23a8-4b79-9a17-447b15b8505f)

**Top 10 Genres by Book Count**
The top book genres are Fiction, Nonfiction, Classics, Historical Fiction, and Romance.
This provides insights into the genre preferences of readers in the dataset.

![image](https://github.com/user-attachments/assets/c7879a9c-73a6-4f9f-86d5-7cbab87912f4)

**Rating Distribution**
The book rating distribution is heavily skewed towards higher ratings, with a peak around 4-4.5 average rating.
This indicates that the dataset contains mostly well-received books.

![image](https://github.com/user-attachments/assets/4016a7a9-a89c-426a-b786-cb13b59196b8)

**Author Frequency**
The top authors by book count include Stephen King, J.K. Rowling, Terry Pratchett, Agatha Christie, and James Patterson.
This highlights the most prolific authors represented in the dataset.

![image](https://github.com/user-attachments/assets/6396f11e-7e47-4095-871b-e4596b0deb8d)

## 🔄 Data Pipeline

**Data Loading and Preprocessing**
Load the dataset using pandas.
Handle missing values in the Description, Genres, and Author columns by replacing them with empty strings.

**Feature Engineering**
Combine key textual features (Description, Genres, Author) into a single feature set for each book.

**TF-IDF Vectorization**
Convert textual data into numerical vectors using the TF-IDF technique to capture the importance of words in the dataset.

**Similarity Matrix**
Compute cosine similarity between book feature vectors to measure their similarity.

**Recommendation System**
Given a book title, find the closest matching title using difflib.
Rank books based on similarity scores and return the top recommendations.

**Data Visualizations**
Generate visualizations for key trends and save them as PNG files.

**Exporting Results**
Export book recommendations to a CSV file for future reference.

## 🚀 Workflow

Step 1: Input a Book Title

The user enters the title of their favorite book.

Step 2: Find Similar Books

The system:

1. Matches the input title with the dataset.
2. Computes similarity scores for all books.
3. Returns the top 30 recommendations.

Step 3: Visualize Insights
Generate visualizations:
1. Top 10 genres.
2. Rating distribution.
3. Similarity heatmap.

Step 4: Export Recommendations
Save the recommendations in a downloadable CSV file.

Step 5: Interactive Gradio App
An easy-to-use interface where users:

Input a book title.
View recommendations, download results, and explore visual insights.

## 🛠️ Tech Stack
Python: Core programming language.

**Libraries**
1. pandas & numpy for data processing.
2. sklearn for TF-IDF vectorization and cosine similarity.
3. matplotlib & seaborn for visualizations.
4. gradio for building the user-friendly app.
5. Data Source: goodreads_data.csv.

## 🌟 Example Usage
Run the app and input a book title (e.g., To Kill a Mockingbird).
View the top 30 book recommendations along with detailed visualizations.
Download a CSV file of the recommendations.
