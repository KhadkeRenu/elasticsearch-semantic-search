# Elasticsearch Semantic Search Engine

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![NLP](https://img.shields.io/badge/NLP-Sentence--Transformers-orange)
![Search](https://img.shields.io/badge/Search-Elasticsearch%20k--NN-005571?logo=elasticsearch)
![Dataset](https://img.shields.io/badge/Dataset-BBC%20News%202%2C225%20articles-green)
![Blogathon](https://img.shields.io/badge/Elastic%20Blogathon-2026-pink)

**Author:** Renuka Khadke
**Published Blog:** [From Dashboards to Intelligent Search with Elasticsearch](https://medium.com/@renuka1996mrch/from-dashboards-to-intelligent-search-with-elasticsearch-52bf4d91e55b)
**Certificate:** Elastic Blogathon 2026 — Elastic Technologies India Pvt. Ltd.

---

## The Problem

Traditional keyword search finds documents containing your **exact query words**.
If you search *"financial crisis"* but the article says *"economic downturn"* — it returns nothing.
The words are different even though the meaning is identical.

## The Solution

This project builds a **semantic search engine** that understands *meaning*, not just words.
Every article is converted into a 384-dimensional vector using Microsoft's sentence-transformer model.
Search finds articles whose vectors are *closest in meaning* to your query — regardless of exact wording.

---

## Results — Semantic vs Keyword Search

**Query:** *"football world cup goals scored"*

| Rank | Keyword Search (BM25) | Semantic Search (k-NN) |
|------|----------------------|------------------------|
| 1 | Brentford v Southampton | Man Utd stroll to Cup win (0.48) |
| 2 | Stuart joins Norwich | Ireland 21-19 Argentina (0.47) |
| 3 | Chelsea sack Mutu | Dundee Utd 4-1 Aberdeen (0.45) |

Keyword search matched random sport articles containing the word "goals."
Semantic search found actual cup/tournament articles by meaning.

---

## Architecture
```
Documents → SentenceTransformer (all-MiniLM-L6-v2) → 384-dim Vectors
                                                              ↓
                                                   Elasticsearch Index
                                                   (dense_vector field)
                                                              ↓
Query → Embed → k-NN Search → Top-K Results ranked by cosine similarity
```

---

## Dataset

**BBC News Archive** — 2,225 real news articles across 5 categories

| Category | Articles |
|----------|----------|
| Sport | 511 |
| Business | 510 |
| Politics | 417 |
| Tech | 401 |
| Entertainment | 386 |
| **Total** | **2,225** |

---

## Visualisations

### 1. Semantic Embedding Space — 2,225 Articles
*Articles cluster by meaning without being told the categories*

![Embedding Space](visualisations/embedding_space_2225.png)

### 2. Article Similarity Matrix
*Same-category articles form green blocks along the diagonal*

![Heatmap](visualisations/similarity_heatmap_2225.png)

### 3. Keyword vs Semantic Comparison
*Same query — completely different results*

![Comparison](visualisations/keyword_vs_semantic_2225.png)

---

## Project Structure
```
elasticsearch-semantic-search/
├── notebooks/
│   └── semantic_search_demo.ipynb   ← full walkthrough
├── src/
│   ├── indexer.py                   ← embeds & indexes documents
│   └── searcher.py                  ← semantic + keyword search
├── visualisations/
│   ├── embedding_space_2225.png
│   ├── similarity_heatmap_2225.png
│   └── keyword_vs_semantic_2225.png
├── requirements.txt
└── README.md
```

---

## Setup
```bash
pip install -r requirements.txt
```

For Elasticsearch production version — add your Elastic Cloud credentials
to `src/indexer.py` and `src/searcher.py`, then:
```bash
python src/indexer.py    # index all documents
python src/searcher.py   # run search queries
```

**Or run the full notebook directly in Google Colab — no setup needed:**
[Open in Colab](https://colab.research.google.com/github/KhadkeRenu/elasticsearch-semantic-search/blob/main/notebooks/semantic_search_demo.ipynb)

---

## Key Concepts

| Concept | Explanation |
|---------|-------------|
| Sentence Embeddings | Text converted to 384 numbers encoding meaning |
| Cosine Similarity | Measures angle between vectors — small angle = similar meaning |
| k-NN Search | Finds k nearest vectors to query in embedding space |
| PCA Projection | Reduces 384 dims → 2D for visualisation |
| BM25 vs k-NN | Keyword overlap vs meaning similarity |

---

## Skills Demonstrated

- NLP & Sentence Embeddings (sentence-transformers, all-MiniLM-L6-v2)
- Vector Search & Similarity (cosine similarity, k-NN, Elasticsearch dense_vector)
- Python (Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn)
- Dimensionality Reduction (PCA visualisation of 384-dim space)
- Data Storytelling (3 custom visualisations explaining the system)

---

## Related

- **Blog:** [From Dashboards to Intelligent Search with Elasticsearch](https://medium.com/@renuka1996mrch/from-dashboards-to-intelligent-search-with-elasticsearch-52bf4d91e55b)
- **Certificate:** Elastic Blogathon 2026 — Elastic Technologies India Pvt. Ltd.
