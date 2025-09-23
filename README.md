# WEEMS: Word Embeddings for Early Modern Science  

---

## Authors

- Vojtěch Kaše  
- Jan Tvrz  
- Jana Švadlenková
- Georgiana Hedesan
- Petr Pavlas  

## License

CC-BY-SA 4.0, see attached `License.md`.

---

## Overview  

This repository provides a series of word vector models trained on two corpora of Early Modern Latin texts:  

- **Noscemus Digital Sourcebook** – a corpus of digitized Early Modern scientific texts in Latin  
  [DOI: 10.5281/zenodo.15040256](https://doi.org/10.5281/zenodo.15040256)  
- **EMLAP** – a corpus of digitized Early Modern Latin Alchemical Prints  
  [DOI: 10.5281/zenodo.14765294](https://doi.org/10.5281/zenodo.14765294)  

For comparison, we also include two publicly available embedding models based on LASLA and Opera Maiora:  
[https://embeddings.lila-erc.eu/#topnav](https://embeddings.lila-erc.eu/#topnav)  

In total, the WEEMS collection offers:  

- 4 temporal models based on NOSCEMUS  
- 8 discipline-specific models based on NOSCEMUS  
- 1 model trained on EMLAP  
- 2 pretrained models (LASLA and Opera Maiora)  

**List of models**  
- NOSCEMUS – 1501–1550  
- NOSCEMUS – 1551–1600  
- NOSCEMUS – 1601–1650  
- NOSCEMUS – 1651–1700  
- NOSCEMUS – Alchemy/Chemistry  
- NOSCEMUS – Astronomy/Astrology/Cosmography  
- NOSCEMUS – Biology  
- NOSCEMUS – Geography/Cartography  
- NOSCEMUS – Mathematics  
- NOSCEMUS – Medicine  
- NOSCEMUS – Meteorology/Earth sciences  
- NOSCEMUS – Physics  
- LASLA  
- Opera Maiora  
- EMLAP  

---

## Data preprocessing  

All models were trained on automatically lemmatized and morphologically annotated sentences, processed with [LatinCy](https://github.com/bmispelon/latincy) (Burns, 2023), which builds on the [spaCy](https://spacy.io) NLP library (Montani et al., 2023).  

- From the corpora, we retained only tokens tagged as **NOUN**, **VERB**, **ADJ**, and **PROPN**.  
- For each subcorpus, we calculated raw lemma frequencies.  
- We then extracted the **5,000 most frequent lemmata per subcorpus**, yielding a combined vocabulary of **11,044 unique words**.  
- During training, items with fewer than **10 occurrences** within a subcorpus were excluded.  

This pipeline ensures that each subcorpus model is both representative of its domain and aligned with a substantial shared vocabulary, making **cross-corpus comparisons** possible.  

Homographs and polysemous lemmata (e.g., *liber* ‘book/free’) are not split into separate vectors, which results in blended representations. This is a known limitation of type-based embeddings and flagged for future refinement.  

---

## Training details  

We employ the **FastText** algorithm with the same parametrization as in:  

> Sprugnoli, R., Moretti, G., & Passarotti, M. (2020). *Building and Comparing Lemma Embeddings for Latin. Classical Latin versus Thomas Aquinas.* *Italian Journal of Computational Linguistics, 6(1).* [DOI: 10.5281/zenodo.4618000](https://doi.org/10.5281/zenodo.4618000)  

This alignment makes WEEMS vectors directly comparable to LASLA and Opera Maiora embeddings.  

The models have been intrinsically evaluated on a standard Latin synonym-selection benchmark, where they achieve high accuracy (≈0.87–0.93 on covered items) across subcorpora, confirming their reliability for both exploratory and comparative research.  

The models are distributed as a single pickle file containing a Python dictionary of Gensim `KeyedVectors`:  

```python
import pickle

with open("../data/vectors_dict_comp.pkl", "rb") as file:
    vectors_dict = pickle.load(file)
```

## Scripts

Scripts and example notebooks are located in the scripts subfolder. Their numbering and titles are self-explanatory. They provide usage examples for loading models, querying nearest neighbors, and reproducing evaluation experiments.

This repository is part of the TOME project.