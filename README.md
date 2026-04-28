# TF-IDF Content-Based Movie Recommender System

This project implements a content-based recommendation engine that suggests movies similar to a given title. It analyzes movie metadata—specifically **genres and keywords**—to understand the thematic essence of a film and find the closest matches in the database.

## 📊 Dataset
The system uses the **TMDB 5000 Movies** dataset, which includes comprehensive metadata for thousands of films, including:
- **Genres:** Action, Adventure, Horror, etc. (stored as JSON).
- **Keywords:** Specific plot elements like "culture clash", "superhero", or "ghost" (stored as JSON).
- **Titles:** Used as the primary lookup for recommendations.

## 🛠 Project Workflow

### 1. Data Cleaning & Parsing
- Movie metadata is often stored in JSON format within the CSV. The project includes a robust parsing function to extract `name` fields from the JSON strings.
- Space-separated names (like "Science Fiction") are condensed (into "ScienceFiction") to ensure the vectorizer treats them as single, unique tokens.

### 2. Feature Engineering
- The cleaned **Genres** and **Keywords** are concatenated into a single "soup" of words for each movie.
- This text "soup" represents the content profile of the movie.

### 3. Vectorization (TF-IDF)
- **TfidfVectorizer:** Converts the text profiles into a sparse matrix of TF-IDF (Term Frequency-Inverse Document Frequency) scores.
- This technique highlights unique, descriptive keywords while down-weighting very common terms.

### 4. Similarity Calculation
- **Cosine Similarity:** The project calculates the cosine of the angle between movie vectors. 
- A score of **1.0** indicates identical content (the movie itself), while scores closer to 1.0 indicate high similarity in genres and themes.

### 5. Recommendation Logic
- A custom `movie_recommender(title)` function:
    1. Locates the index of the input movie.
    2. Retrieves its similarity scores against all other movies.
    3. Sorts the scores in descending order.
    4. Returns the top 5 most similar titles (excluding the input movie itself).

## 🚀 Examples
- **Input:** `Iron Man` -> **Recommendations:** `Iron Man 2`, `Ant-Man`, `Iron Man 3`, `Thor: The Dark World`, `Captain America: Civil War`.
- **Input:** `The Conjuring` -> **Recommendations:** `The Haunting in Connecticut 2`, `The Woman in Black`, `The Vatican Exorcisms`.

## ⚙️ Setup & Requirements
- **Dependencies:** `pandas`, `numpy`, `scikit-learn`, `matplotlib`.
- **Run:** Open `TFIDF Movie Recommender System.ipynb` in Jupyter and run the cells. Ensure `tmdb_5000_movies.csv` is in the same directory.
