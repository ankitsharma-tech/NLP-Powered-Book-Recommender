# 📚 Book Recommendation System using NLP

An advanced web-based **Natural Language Processing (NLP)** mini-project that delivers personalized book recommendations by combining **popularity metrics**, **collaborative filtering**, and **NLP-driven text analysis**. Developed as part of the **SEM-VII NLP Lab**, this system demonstrates how NLP techniques and machine learning algorithms can work together to enhance content discovery in a modern web application.

---

## 📢 About the Project

Readers today face an ever-growing library of options. To help users find books aligned with their interests, this project leverages:  
1. **Popularity-Based Recommendations** – surfaces the top 50 books by aggregate ratings and votes.  
2. **Collaborative Filtering** – identifies books similar to a user’s favorite based on collective user preferences.  
3. **NLP Techniques** – preprocesses and analyzes textual metadata (titles, descriptions) to enrich the recommendation pipeline and ensure robust data handling.

The entire application is built using **Flask** for backend routing and templating, with a **Bootstrap** frontend for responsive design. Models are trained and serialized in **Google Colab**, then deployed locally via Flask.

---

## 🎯 Project Objectives

- **Web Application Development**  
  Build a Flask-based interface where users can browse popular titles and request personalized suggestions.

- **NLP Pipeline Implementation**  
  Apply text-processing steps (lowercasing, stop-word removal) to book metadata to ensure clean, structured inputs for modeling.

- **Machine Learning Integration**  
  Train and serialize:
  - A **popularity model** (top-50 extraction)
  - A **collaborative filtering model** (cosine similarity on user-item ratings)

- **Model Serialization for Fast Retrieval**  
  Use **Pickle** to store precomputed matrices (`popular.pkl`, `similarity_scores.pkl`, `pt.pkl`) for sub-second recommendations.

- **Responsive UI/UX**  
  Design HTML templates (`index.html`, `recommend.html`) with Bootstrap to provide an intuitive and mobile-friendly experience.

- **Scalability & Extensibility**  
  Structure code and data storage to accommodate growing datasets, additional NLP models, and future feature extensions (e.g., user authentication, real-time feedback).

---

## 🧠 Problem Statement

> **Challenge:** Users are overwhelmed by millions of titles and lack effective tools to navigate this content.  
> **Solution:** Combine popularity insights with personalized, NLP-enhanced algorithms to recommend books that match both general trends and individual tastes.

---

## 🛠️ Prerequisites & Tools

Before running the project, ensure you have the following:

- **Programming Language:** Python 3.x  
- **Development Platform:**  
  - **Model Training:** Google Colab (cloud-based Jupyter notebooks)  
  - **App Deployment:** Local machine (Windows 10/11 or Ubuntu 20.04+)  
- **Backend Framework:** Flask  
- **Frontend:** HTML5, CSS3, Bootstrap 3.3.7  
- **Libraries & Packages:**  
  - **Data Handling & ML:** pandas, numpy, scikit-learn  
  - **Serialization:** pickle  
  - *(Optional for extended NLP):* NLTK, spaCy  
- **Datasets:** CSV files (`books.csv`, `users.csv`, `ratings.csv`)  
- **Version Control:** Git & GitHub for code and report hosting

---

## 🧩 System Architecture

1. **Data Layer**  
   - **Books Dataset:** ID, title, author, description, image URL  
   - **Users Dataset:** ID, demographic info (for future NLP persona modeling)  
   - **Ratings Dataset:** User–book rating pairs  

2. **Business Logic Layer**  
   - **NLP Preprocessor:**  
     - Lowercasing, punctuation removal  
     - (Optional) Tokenization & stop-word removal  
   - **Popularity Model:** Aggregates number of ratings & mean rating → Top-50 list → `popular.pkl`  
   - **Collaborative Filtering Model:**  
     - Pivot table (books × users) → Cosine similarity matrix → `similarity_scores.pkl`  

3. **Presentation Layer**  
   - **Routes:**  
     - `/` → Renders `index.html` with Top-50 books  
     - `/recommend` (GET) → Shows search form  
     - `/recommend_books` (POST) → Returns personalized suggestions  
   - **Templates:** Bootstrap cards display book covers, titles, authors, ratings
  
---

## 📚 Datasets

| Dataset          | Description                                                             |
|------------------|-------------------------------------------------------------------------|
| `books.csv`      | Contains metadata: `Book-Title`, `Book-Author`, `Image-URL-M`, `Description` |
| `users.csv`      | Contains simple user IDs and demographic fields                          |
| `ratings.csv`    | Contains `User-ID`, `Book-ID`, and `Rating`                              |

*All datasets sourced from Kaggle’s “Book Recommendation Dataset.”*

---

## 🔎 Algorithms & Methodologies

### 1. Popularity-Based Recommendation

- **Objective:** Surface books with broad appeal.  
- **Pipeline:**  
  1. Aggregate `ratings.csv` to compute total votes and average rating per book.  
  2. Filter out books with fewer than 250 votes (to ensure statistical reliability).  
  3. Sort by descending average rating.  
  4. Serialize the Top-50 into `popular.pkl`.

---

### 2. Collaborative Filtering (Item-Based)

- **Objective:** Recommend titles similar to a user-selected book.  
- **Pipeline:**  
  1. Build a pivot table (`pt.pkl`): rows = book titles, columns = user IDs, values = ratings.  
  2. Compute pairwise cosine similarity on this sparse matrix.  
  3. Store similarity scores in `similarity_scores.pkl` for O(1) lookup.  
  4. On user input, retrieve top-4 most similar books (excluding the query itself).

---

### 3. NLP Techniques (Data Hygiene & Enrichment)

- **Data Cleaning:** Lowercasing, strip HTML/entities from descriptions.  
- **(Optional) Tokenization & Stop-Word Removal:** Prepare text for advanced NLP modules (e.g., embedding-based similarity).  
- **Future Scope:** TF-IDF vectorization or transformer embeddings (spaCy, BERT) to enable content-based recommendations alongside collaborative methods.

---

## 🔥 Implementation Details

1. **Model Training (Google Colab)**  
   - Load raw CSVs → Clean & normalize → Train popularity & collaborative filtering models → Serialize with Pickle.

2. **Flask App (Local)**  
   - Load `popular.pkl`, `pt.pkl`, `similarity_scores.pkl`.  
   - Define routes (`/`, `/recommend`, `/recommend_books`).  
   - Render templates with data passed from backend logic.

3. **Templates & Styling**  
   - `index.html`: Displays Top-50 in a 4-column Bootstrap grid.  
   - `recommend.html`: Search form + recommendation cards; includes client-side validation/clear functionality.

4. **Error Handling & UX**  
   - Alerts for invalid or missing user input.  
   - Graceful messages if no similar books found.

---

## 🛠️ Future Scope

- **Content-Based NLP Models:** Incorporate TF-IDF vectors or BERT embeddings on `Description` to recommend by semantic similarity.  
- **Hybrid Recommender:** Combine collaborative filtering, popularity, and content-based scores.  
- **User Profiles & Feedback Loops:** Enable sign-in, track user history, refine recommendations over time.  
- **Multilingual Descriptions:** Extend NLP pipeline to support non-English metadata.  
- **Real-Time Updates:** Auto-retrain/recompute similarity as new ratings arrive.