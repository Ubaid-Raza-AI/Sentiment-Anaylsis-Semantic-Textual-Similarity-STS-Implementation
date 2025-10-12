# Sentiment & STS Implementation

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **A streamlined pipeline that analyzes game reviews, combines negative ones, and refines them using semantic similarity techniques for advanced language model processing.**

## Project Overview

This project implements sentiment analysis techniques to classify game reviews, aggregates negative reviews for each game, and applies semantic textual similarity methods to condense and refine the combined reviews—preparing them for advanced language models such as GPT for further analysis and summarization.

## Dataset Description

The project utilizes a structured dataset of video game reviews sourced from public scraping efforts. Key details:

- **Essential Columns**:
  - **Game Name**: The title of the video game (used for grouping and identification).
  - **Review**: The raw textual review content (core input for processing).

- **Exploratory Column**:
  - **Genre**: Provided for optional genre-based exploration (e.g., visualizing distribution across genres). This column is **not utilized in the main analysis pipeline** to keep the focus on review content and game-specific insights.

The dataset is loaded as an Excel file (`Sample_Dataset_of_games.xlsx`) with rows representing individual reviews. For privacy and compliance, ensure your usage aligns with data sourcing terms.

**Sample Structure**:
| Game Name       | Review                          | Genre    |
|-----------------|---------------------------------|----------|
| Example Game 1 | "The controls feel clunky..."  | Action  |
| Example Game 2 | "Great story but buggy..."     | RPG     |

## Methodology / Workflow

The pipeline follows a clean, step-by-step process to transform raw reviews into actionable summaries:

1. **Data Loading & Cleaning**: Load the dataset, drop null reviews, and explore basic stats (e.g., unique games per genre for context).
2. **Sentiment Analysis**: Apply multiple techniques (TextBlob, VADER, Naive Bayes via NLTK, and BERT-based classification) to categorize reviews as positive, negative, or neutral. This step identifies negative reviews for focused analysis.
3. **Evaluation of Sentiment Analysis**: Assess the performance of each technique using AUC scores to select the most reliable method (VADER) for downstream filtering.
4. **Review Aggregation**: Group reviews by game, focusing on negative feedback to build comprehensive per-game corpora.
5. **Text Preprocessing**: Normalize text by lowercasing, removing noise (e.g., digits, special characters), tokenizing, and applying stemming/lemmatization for cleaner input.
6. **Semantic Reduction via STS**: Employ sentence-level similarity models to detect and merge overlapping content, reducing redundancy while preserving core meaning.
7. **Evaluation**: Assess summary quality using metrics like ROUGE, BLEU, METEOR, and BERT-Score to ensure fidelity to originals.
8. **Output Generation**: Produce refined summaries saved as Excel files for easy review.

This approach ensures summaries are concise yet informative, typically reducing word count by 50-70% without losing critical insights.

## Technologies Used

- **Python 3.8+**: Core programming language.
- **Pandas & NumPy**: Data manipulation and analysis.
- **TextBlob & VADER**: For polarity-based and lexicon-based sentiment analysis.
- **Transformers (Hugging Face)**: Pre-trained models for BERT-based sentiment classification.
- **Sentence Transformers**: For semantic embeddings and similarity computation.
- **ROUGE-Score & BERT-Score**: Automated evaluation of summary quality.
- **Scikit-learn**: For AUC score computation in sentiment evaluation.
- **Other Utilities**: BeautifulSoup for cleaning.

Full dependencies are listed in `requirements.txt`.

## Results / Outputs

The system generates per-game negative review summaries, highlighting common criticisms (e.g., "buggy mechanics and poor optimization"). Key outputs include:

- **Sentiment Results**: DataFrames with classified sentiments and AUC evaluation prints (e.g., AUC for VADER: ~0.85).
- **Preprocessed Data**: Cleaned review corpora (`textpreprocessing_summaries.xlsx`).
- **Reduced Summaries**: STS-optimized versions (`sentencetransformer.xlsx`, `sbert.xlsx`, `sebert.xlsx`).
- **Final Insights**: Consolidated summaries (`summariesofgames.xlsx`) ready for qualitative analysis.
- **Evaluation Metrics**: Printed scores (e.g., ROUGE-1 F1: ~0.65) validating summary coherence.

These outputs enable rapid trend spotting, such as recurring issues in gameplay or UI across titles.

## How to Run the Project

### Prerequisites
- Python 3.8+ installed.
- Access to Google Colab (recommended for GPU acceleration) or a local environment.

### Quick Start
1. **Clone the Repo**:
   ```
   git clone https://github.com/Ubaid-Raza-AI/Sentiment-Anaylsis-Semantic-Textual-Similarity-STS-Implementation-.git
   cd Sentiment-STS-Implementation
   ```

2. **Install Dependencies**:
   ```
   pip install -r requirements.txt
   ```

3. **Prepare Data**:
   - Place your `Sample_Dataset_of_games.xlsx` in the root directory (or `/content/` for Colab).

4. **Run the Script**:
   - In Colab: Upload the script and data, then execute cells sequentially.
   - Locally: `python main.py` (rename the refactored script accordingly).
   - Expected runtime: ~10-20 minutes for a dataset of 1,000+ reviews (depending on hardware).

5. **View Outputs**:
   - Check generated Excel files in the root or `/content/` directory.

**Troubleshooting**: If additional models are needed, run `python -m spacy download en_core_web_lg` post-install.

## Future Improvements

- Integrate advanced LLMs (e.g., GPT variants) for abstractive summarization beyond extractive STS.
- Add visualization dashboards (e.g., via Streamlit) for interactive review exploration.
- Expand to multi-lingual support or real-time processing for live review streams.
- Incorporate user feedback loops to refine similarity thresholds dynamically.

Contributions via pull requests are welcome!

## License and Credits

This project is licensed under the MIT License—feel free to use, modify, and distribute.

**Credits**:
- Developed by Ubaid Raza as part as an NLP project for game analytics.
- Inspired by open-source Hugging Face models and evaluation benchmarks.
- Dataset credits: [Source if applicable, e.g., public scraping from Steam/IGN].

---

Star this repo if it helps your NLP projects!
