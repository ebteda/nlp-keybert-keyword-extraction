# Data

The datasets are **not** in this repository. This page says what each one is and where to get it.

---

## 1. SemEval-2010 Task 8 (main dataset)

**What it is:** short English sentences. In each sentence, **two words are marked** with tags, like this:

```
The <e1>child</e1> was carefully wrapped and bound into the <e2>cradle</e2> by means of a cord.
```

The dataset was made for a different task (finding the relation between the two words). We used the two marked words as the **true keywords** of the sentence.

**Size:** 8,000 sentences for train, 2,717 for test.

**How we used it:**
- We remove the tags, give the sentence to KeyBERT, and compare its keywords with the two marked words.
- Every sentence has **exactly 2** marked words, so KeyBERT picks 2 keywords.
- A marked word is **at most 3 words long** (for example `stem cell research`). That is why we tried phrases up to 3 words.
- Used in notebooks 01 to 06.

**Download:** it downloads by itself in the notebooks, from Hugging Face:

```python
from datasets import load_dataset
ds = load_dataset("SemEvalWorkshop/sem_eval_2010_task_8")
```

Dataset page: [SemEval-2010 Task 8 on Hugging Face](https://huggingface.co/datasets/SemEvalWorkshop/sem_eval_2010_task_8)

---

## 2. KPTimes (new-domain test)

**What it is:** news articles (mostly from the New York Times), with keywords chosen by the editors. About 260,000 articles for train and 20,000 for test.

**How we used it:** only in notebook 07. We kept a small, clean part of it:
- only **sports** articles,
- only keywords that really **appear in the text**,
- articles with **at most 300 words** and **at most 4 keywords**,
- keywords **at most 3 words** long.

That left **9,125 train** and **341 test** articles, about **114 words** long on average. KeyBERT picks **3 keywords** for each article.

**Download:** [KPTimes on GitHub](https://github.com/ygorg/KPTimes)

Put the two files here, next to the notebooks:

```
codes/
└── data/
    ├── KPTimes.train.jsonl
    └── KPTimes.test.jsonl
```

---

## Models

All models download by themselves the first time you run a notebook (from Hugging Face):

| Model | Used in |
|---|---|
| KeyBERT default (all-MiniLM-L6-v2) | notebooks 01 to 04 |
| all-mpnet-base-v2, paraphrase-MiniLM-L6-v2, roberta-base, roberta-large, albert-base-v2 | notebooks 05 and 06 |
| paraphrase-MiniLM-L6-v2 | notebook 07 |
