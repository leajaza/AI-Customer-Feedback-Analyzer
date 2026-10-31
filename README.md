# AI-Powered Customer Feedback Analyzer

An end-to-end Generative AI application that analyzes customer feedback using **Google Gemini**, **FastAPI**, **Streamlit**, and **SQLite**.

The application helps businesses understand customer satisfaction by automatically identifying sentiment, assigning satisfaction scores, and extracting common feedback themes.

## Overview

Businesses often receive large amounts of customer feedback, making it difficult to manually analyze every review and identify recurring issues.

This project simplifies that process through an AI-powered dashboard where users can submit multiple customer reviews and instantly receive structured insights.

Each review is analyzed using Google's Gemini model, and the results can be stored in a local database for future reference.

## Key Features

- **AI-Powered Sentiment Analysis:** Classifies customer reviews as positive, negative, or neutral.
- **Customer Satisfaction Scoring:** Assigns a score from 1 (very negative) to 5 (very positive).
- **Theme Extraction:** Identifies the main topic of each review, such as delivery, taste, price, or service.
- **Batch Review Processing:** Analyzes multiple customer reviews in one session.
- **Interactive Dashboard:** Displays analysis results in an easy-to-use Streamlit interface.
- **Summary Statistics:** Calculates the total number of reviews, average satisfaction score, and percentage of positive feedback.
- **Common Theme Detection:** Identifies the most frequently mentioned feedback topic.
- **Database Storage:** Saves analyzed reviews in SQLite and allows users to access previous results.
- **Error Handling:** Handles unsuccessful review analyses without stopping the entire batch.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Google Gemini API | AI-powered sentiment analysis and theme extraction |
| FastAPI | Backend API development |
| Streamlit | Interactive web dashboard |
| Pydantic | Input validation and structured AI output |
| SQLite | Local database for storing analyzed reviews |
| Requests | HTTP communication between frontend and backend |
| Python-dotenv | Environment variable management |
| UV | Python dependency and environment management |

## System Architecture

The application consists of a frontend, backend, AI integration, and database layer.

**Workflow:**

1. The user enters customer reviews into the Streamlit dashboard.
2. Streamlit sends each review to the FastAPI backend through an HTTP POST request.
3. FastAPI forwards the review and analysis instructions to Gemini.
4. Gemini generates structured results containing sentiment, score, and theme.
5. FastAPI returns the results to Streamlit.
6. Streamlit displays the analyses and calculates summary statistics.
7. The user can save the results to SQLite and retrieve previously stored reviews.

**Architecture:**

```text
        Customer Reviews
               |
               v
     Streamlit Frontend
           (app.py)
               |
          HTTP POST
               |
               v
       FastAPI Backend
           (api.py)
               |
               v
         Gemini API
               |
               v
      Structured Analysis
     (label, score, theme)
               |
               v
      Streamlit Dashboard
               |
        Save / Retrieve
               |
               v
        SQLite Database
         (database.py)
```

## Project Structure

```text
Project_Feedback_Analyzer/
│
├── api.py
├── app.py
├── database.py
├── sample_reviews.txt
├── pyproject.toml
├── uv.lock
├── .gitignore
└── README.md
```

Additional local files:

- `.env` — Stores the Gemini API key and must not be committed to Git.
- `feedback.db` — SQLite database created when the application runs.
- `.venv/` — Local Python virtual environment.

## Installation and Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd Project_Feedback_Analyzer
```

Replace `<repository-url>` with the GitHub repository URL.

### 2. Install dependencies

Install UV if it is not already installed.

Then run:

```bash
uv sync
```

This installs the project's Python dependencies.

### 3. Configure the Gemini API key

Create a `.env` file in the project's root directory.

Add:

```env
GEMINI_API_KEY=your_gemini_api_key
```

Generate an API key through Google AI Studio.

**Security:** Never upload your actual API key to GitHub. Ensure `.env` is included in `.gitignore`.

### 4. Start the FastAPI backend

Open a terminal and run:

```bash
uv run fastapi dev api.py
```

The backend will normally run at:

`http://127.0.0.1:8000`

FastAPI's interactive documentation is available at:

`http://127.0.0.1:8000/docs`

### 5. Start the Streamlit frontend

Open a second terminal and run:

```bash
uv run streamlit run app.py
```

The application will normally open at:

`http://localhost:8501`

Keep both terminals running while using the application.

## Example

**Input customer review:**

```text
The food was delicious but the delivery took over an hour. Not happy.
```

**Example AI-generated output:**

```json
{
  "label": "negative",
  "score": 2,
  "theme": "delivery"
}
```

The model identifies the review as negative, assigns a satisfaction score, and extracts delivery as the main topic.

### Dashboard Results

In a test using four sample customer reviews, the application produced:

| Metric | Result |
|---|---|
| Total Reviews | 4 |
| Average Satisfaction Score | 2.2 / 5 |
| Positive Reviews | 25% |
| Most Common Theme | Delivery |

The dashboard also provides an option to save all analyzed reviews to `feedback.db` and display their saved history.

## What I Learned

Building this project helped me gain practical experience with:

- Developing REST API endpoints using FastAPI.
- Connecting Python applications to an external LLM through an API.
- Designing structured AI outputs using Pydantic.
- Building interactive web interfaces using Streamlit.
- Sending HTTP POST requests between frontend and backend components.
- Performing database operations using SQLite.
- Managing virtual environments and dependencies using UV.
- Debugging API errors, model availability issues, and usage limits.
- Understanding how different components work together in an end-to-end AI application.

## Future Improvements

Potential enhancements include:

- Adding charts to visualize sentiment distribution and common themes.
- Filtering reviews by sentiment category.
- Supporting CSV or text file uploads.
- Generating AI-powered recommendations for improving customer satisfaction.
- Exporting analysis reports.
- Deploying the application online.

## Acknowledgment

This project was developed as a hands-on learning exercise while following the **Codebasics Python for AI tutorial**.

The project provided practical experience in understanding, integrating, testing, and debugging an AI-powered application using Python and modern development tools.