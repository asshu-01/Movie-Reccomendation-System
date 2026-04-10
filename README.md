# Movie Recommendation System

A full-stack movie recommendation application that combines:

- Content-based recommendations using TF-IDF and cosine similarity
- Real-time movie metadata from TMDB
- An interactive Streamlit frontend
- A FastAPI backend for search, details, and recommendations

Live Demo: https://movie-reccomendation-system-5.streamlit.app/

## Overview

This project helps users discover movies through two recommendation strategies:

- Similar Movies (TF-IDF): Recommends titles based on textual similarity from a local movie dataset
- Genre-Based Suggestions (TMDB): Recommends trending movies from similar genres using TMDB data

Users can search for a movie, view details, and instantly get recommendation grids with posters.

## Features

- Keyword movie search with suggestions
- Home feed categories:
	- Trending
	- Popular
	- Top Rated
	- Now Playing
	- Upcoming
- Movie details view with poster, backdrop, release date, genres, and overview
- Hybrid recommendation flow:
	- TF-IDF recommendations from local model artifacts
	- TMDB genre recommendations from live API
- Clean Streamlit UI with grid layout and detail navigation

## Tech Stack

- Frontend: Streamlit
- Backend: FastAPI, Uvicorn
- ML/Data: scikit-learn, pandas, numpy, scipy
- External API: TMDB (The Movie Database)
- HTTP Client: httpx, requests

## Project Structure

.
|- app.py                   # Streamlit frontend
|- main.py                  # FastAPI backend
|- requirements.txt         # Python dependencies
|- runtime.txt              # Deployment runtime (Python 3.11.9)
|- .python-version          # Local Python version
|- movies_metadata.csv      # Source metadata
|- df.pkl                   # Processed movie dataframe
|- indices.pkl              # Title-to-index mapping
|- tfidf.pkl                # TF-IDF vectorizer
|- tfidf_matrix.pkl         # TF-IDF matrix
|- Movies.ipynb             # Notebook for experimentation/training

## How It Works

1. User searches for a movie in the Streamlit app.
2. FastAPI fetches matching titles from TMDB.
3. Selected movie details are loaded by TMDB ID.
4. Backend computes TF-IDF recommendations from local model artifacts.
5. Backend also fetches genre-based recommendations from TMDB.
6. Frontend renders both recommendation sections with posters.

## API Endpoints

Base backend (example): https://movie-reccomendation-system-t7r1.onrender.com/

- GET /health
- GET /home?category=popular&limit=24
- GET /tmdb/search?query=batman&page=1
- GET /movie/id/{tmdb_id}
- GET /recommend/genre?tmdb_id=550&limit=18
- GET /recommend/tfidf?title=Inception&top_n=10
- GET /movie/search?query=Inception&tfidf_top_n=12&genre_limit=12

## Local Setup

### 1. Clone Repository

```bash
git clone https://github.com/asshu-01/Movie-Reccomendation-System.git
cd Movie-Reccomendation-System
```

### 2. Create and Activate Virtual Environment

Windows:

```bash
python -m venv myenv
myenv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a .env file in the project root:

```env
TMDB_API_KEY=your_tmdb_api_key_here
```

### 5. Run Backend

```bash
uvicorn main:app --reload
```

Backend default URL: http://127.0.0.1:8000

### 6. Run Frontend

```bash
streamlit run app.py
```

Frontend default URL: http://localhost:8501

## Deployment Notes

- Streamlit app is deployed and publicly accessible at:
	- https://movie-reccomendation-system-5.streamlit.app/
- Backend API can be deployed on Render (or similar) and should expose FastAPI routes.
- Keep TMDB_API_KEY configured in deployment environment variables.

## Future Improvements

- Add user ratings and personalization
- Add filtering by language, year, and vote average
- Improve ranking by combining TF-IDF and TMDB popularity signals
- Add test suite for API and recommendation logic

## Author

Ashutosh

## License

This project is for educational and portfolio purposes.
