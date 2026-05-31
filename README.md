# clinical-nlp-basics

Personal learning notebook covering NLP fundamentals with a clinical text focus. Built while preparing for an NLP internship at a clinical AI company.

Not a project — just notes + working code from ground up.

---

## what's covered

**Text basics**
- Tokenization and text cleaning with NLTK
- Stopword removal, lemmatization
- TF-IDF vectorization on clinical documents

**Word embeddings**
- Word2Vec from scratch on clinical sentences
- Semantic similarity between medical terms

**Transformers**
- BioBERT tokenization — how clinical text gets split into subword tokens
- Extracting `[CLS]` embeddings for sentence-level representation
- Why context-aware embeddings matter for clinical text (negation, ambiguity)

**Named Entity Recognition**
- spaCy general NER vs HuggingFace biomedical NER (`d4data/biomedical-ner-all`)
- Structured entity extraction: drugs, diseases, dosages from free-form clinical notes
- Fixing label schema mismatches between off-the-shelf models and task requirements

**Text Classification**
- Adverse event detection: TF-IDF + Logistic Regression baseline
- Same task with BioBERT `[CLS]` embeddings + Logistic Regression
- Comparison: TF-IDF gets 100% accuracy at 50-55% confidence; BioBERT gets 90% accuracy at 95-99% confidence — the difference between memorising words and understanding meaning

---

## stack

```
transformers==4.x
torch
spacy + en_core_web_sm
gensim
nltk
scikit-learn
```

---

## key observation

TF-IDF and BERT were compared on the same adverse event classification task. TF-IDF hit perfect accuracy on the test set but was barely above 50% confident on sentences with unseen phrasing. BioBERT embeddings were consistently 90-99% confident because they encode meaning, not word frequency. In clinical text where negation and synonyms are everywhere, that difference matters.

---

## models used

- `dmis-lab/biobert-base-cased-v1.2` — BioBERT for embeddings
- `d4data/biomedical-ner-all` — biomedical NER
- `deepset/roberta-base-squad2` — extractive QA
