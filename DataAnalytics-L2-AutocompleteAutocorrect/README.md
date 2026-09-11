# DataAnalytics-L2-AutocompleteAutocorrect

Name: Godword Adjei
Track: Data Analytics
Level: 2
Task: Autocomplete and Autocorrect Data Analytics
Internship: Oasis Infobyte — OIBSIP

## Objective

Analyze the efficiency and accuracy of autocomplete and autocorrect algorithms using NLP: implement and compare multiple approaches for next-word prediction and spelling correction on a real text corpus.

## Dataset

| | |
|---|---|
| Source | NLTK's built-in Project Gutenberg corpus (public-domain classic literature — Austen, Shakespeare, Melville, and others) |
| Loading | Downloaded automatically via `nltk.download("gutenberg")` — no manual file needed |
| Corpus size | ~2.6 million tokens after cleaning (alphabetic tokens only) |

## Tools

Python · NLTK (tokenization, n-grams) · pyspellchecker · pandas · Matplotlib · Seaborn · Jupyter Notebook

## What the notebook does

- **Preprocessing** — lowercasing, tokenization, and removal of punctuation/numeric tokens
- **Word frequency analysis** — top 20 most frequent words in the corpus, visualized
- **Autocomplete** — a frequency-based bigram/trigram model: given a 1-2 word prefix, returns the top 3 most likely next words, tested on 10 example prefixes
- **Autocorrect** — two approaches compared on 20 deliberately misspelled words:
  1. `pyspellchecker` (frequency-weighted edit-distance correction)
  2. A custom Levenshtein-distance nearest-neighbor search (no frequency weighting)
- **Performance metrics** — accuracy for both autocorrect approaches, exported and charted
- **Discussion** — limitations of this approach compared to production systems (Google Keyboard, iOS predictive text)

## Results

**Autocomplete — sample predictions** (full results in `outputs/autocomplete_results.csv`):

| Prefix | Top 3 predictions |
|---|---|
| "i am" | sure, the, not |
| "in the" | land, midst, world |
| "my dear" | i, emma, sir |

("emma" appears because Jane Austen's *Emma* is part of the corpus — the model is genuinely picking up context from the training text.)

**Autocorrect — accuracy on 20 misspelled test words:**

| Method | Accuracy |
|---|---|
| **pyspellchecker** (frequency-weighted) | **65%** |
| Custom Levenshtein (distance-only) | 40% |

**Key finding:** frequency weighting matters — when multiple candidate corrections are within the same edit distance, picking the more common word in the corpus resolves ambiguity that pure edit-distance cannot, which explains the 25-point accuracy gap between the two methods.

## Limitations vs. production systems

This project demonstrates the core mechanisms, but production tools like Google Keyboard differ in key ways: they personalize to individual users, use much larger context windows (often transformer-based language models rather than n-grams), factor in keyboard-layout proximity for likely typos, and use scalable data structures (tries/BK-trees) instead of a brute-force vocabulary search. See the notebook's final section for the full discussion.

## Files

```
DataAnalytics-L2-AutocompleteAutocorrect/
├── AutocompleteAutocorrect.ipynb   # main notebook
├── README.md
├── data/                            # empty — corpus loads via nltk.download(), no manual file needed
└── outputs/
    ├── autocomplete_results.csv
    ├── autocorrect_results.csv
    ├── autocorrect_metrics.csv
    ├── 01_top20_words.png
    └── 02_autocorrect_comparison.png
```

## How to run

```bash
pip install -r ../requirements.txt
jupyter notebook AutocompleteAutocorrect.ipynb
```

Then Cell → Run All. (NLTK will auto-download the Gutenberg corpus on first run.)

## Demo video

(paste your LinkedIn post URL here)

#oasisinfobyte
