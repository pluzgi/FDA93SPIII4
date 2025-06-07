# 🧠 Reflective Writing Analysis Pipeline

This project provides a comprehensive data analysis pipeline for exploring, cleaning, enriching, and analyzing student-written reflections from a multilingual dataset. The primary goal is to quantify reflection depth and examine linguistic indicators of reasoning and growth.

---

## 📁 Project Structure

```
project/
├── input/
│   └── dataset_rflect.xlsx            # Original raw dataset
├── output/
│   └── rflect_data_profile.html       # Auto-generated profiling reports
│   └── final_reflection_dataset.csv
├── nltk_data/                         # Custom NLTK data folder for portability
├── main.py                            # Core data pipeline (the code)
└── README.md
```

---

## 🔧 Requirements

Install all dependencies:

```bash
pip install -r requirements.txt
```

Make sure nltk has access to required models:

```bash
python -c "import nltk; nltk.download('punkt')"
```

---

## 📊 Pipeline Overview

### Data Loading
- Loads Excel file from `input/` directory
- Sets up output directories

### Profiling (optional)
- Generates `ydata_profiling` report for initial dataset overview (disabled by default)

### Data Cleaning & Deduplication
- Filters out rows with missing or trivial final reflections
- Removes duplicate entries, preserving only the most recent per unique reflection

### Text Normalization
- Strips HTML tags and whitespace from text fields
- Adds cleaned versions of text fields with character length metrics

### Language Detection
- Uses `langdetect` to identify the language of each reflection
- Supports `en`, `de`, `fr`, `nl` with custom NLTK sentence tokenizers

### Feature Engineering
Calculates:
- Word/sentence counts
- Lexical diversity
- LIX readability index
- Reasoning keyword and phrase occurrences
- Frequency of "I" statements

### Reflection Depth Scoring
- Heuristic scoring to rate reflection depth as: **Low**, **Moderate**, or **High**

### Exploratory Visualization
- Interactive analysis using `pygwalker`
- Boxplots comparing features across reflection depth levels
- Kruskal-Wallis tests to assess feature differences

### Snapshot vs Final Reflection Analysis
- Computes delta metrics between initial and final reflections
- Performs Spearman correlation analysis to explore relationships between change metrics and reflection quality

---

## 📤 Outputs

- `final_reflection_dataset.csv`: Cleaned, enriched dataset with engineered features and depth categorization
- Correlation heatmaps and statistical summaries

---

## 🔬 Key Features Extracted

| Feature                   | Description                                       |
|---------------------------|---------------------------------------------------|
| `word_count_final`        | Word count of the final reflection                |
| `sentence_count_final`    | Sentence count (language-specific)                |
| `lexical_diversity_final` | Unique words / total words                        |
| `readability_lix_final`   | LIX readability index                             |
| `reasoning_keywords_final`| Count of reasoning keywords                       |
| `i_statements_final`      | Number of sentences starting with "I"            |
| `depth_score`             | Composite score from rules                        |
| `depth_category`          | Categorized as Low/Moderate/High                 |

---

## 📈 Example Visuals

- Boxplots of linguistic features across reflection depths
- Heatmap of Spearman correlations between reflection changes and final quality
- Interactive EDA with PyGWalker

---

## 🛠 Development Notes

- All computations are offline and language-aware.
- Designed for notebook environments but can run in standalone scripts.
- Easily extendable for new languages, features, or models.
