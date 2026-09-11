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
| Raw files | data/ — 18 source texts (887KB–4.3MB each, 11.8MB total), exported directly from `nltk.corpus.gutenberg` for transparency/offline reproducibility |
| Loading | The notebook itself still fetches the corpus via `nltk.download("gutenberg")` at runtime (auto-downloads on first run) — the files in `data/` are an exact copy of what that call retrieves |
| Corpus size | ~2.1 million tokens after cleaning (alphabetic tokens only) |

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
| **pyspellchecker** (frequency-weighted) | **75%** |
| Custom Levenshtein (distance-only) | 65% |

**Key finding:** frequency weighting helps but doesn't dominate — pyspellchecker's edge comes from breaking edit-distance ties using word frequency (e.g. for "adress", both "address" and "dress" are one edit away; frequency favors the wrong one here, showing this isn't a guaranteed win). The larger remaining error source for *both* methods is words with genuine ties at distance 1 with no frequency signal to break them correctly (e.g. "familys" → "family" instead of "families", "childs" → "child" instead of "children") — a structural limitation of edit-distance-based correction, not something either method's tie-breaking rule can fully fix.

**Note on test-set design:** four originally-planned test words (`untill`, `frend`, `comming`, `truely`) were replaced after discovering they are archaic-but-valid spelling variants that actually occur in this 19th-century corpus (e.g. "comming" appears 13 times) — both methods would have "correctly" left them unchanged relative to their own reference vocabulary, which would have deflated both accuracy scores for a reason unrelated to the algorithms being compared. The notebook verifies each replacement word is absent from the corpus vocabulary before using it. Also fixed: the custom method originally broke edit-distance ties using Python's randomized set iteration order, making results non-reproducible between runs — it now iterates the vocabulary in sorted order for a deterministic (if still imperfect) tie-break.

## Limitations vs. production systems

This project demonstrates the core mechanisms, but production tools like Google Keyboard differ in key ways: they personalize to individual users, use much larger context windows (often transformer-based language models rather than n-grams), factor in keyboard-layout proximity for likely typos, and use scalable data structures (tries/BK-trees) instead of a brute-force vocabulary search. See the notebook's final section for the full discussion.

## Files

```
DataAnalytics-L2-AutocompleteAutocorrect/
├── AutocompleteAutocorrect.ipynb   # main notebook
├── README.md
├── data/                            # 18 raw Gutenberg text files (auto-fetched by the notebook too)
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



#oasisinfobyte
