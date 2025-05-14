# WEEMS: Word Embeddings for Early Modern Science 

---

## Authors

* Vojtěch Kaše, Jan Tvrz, Jana Švadlenková, Petr Pavlas

## License

CC-BY-SA 4.0, see attached License.md

---

In this repository, we train and make available for reuse by other scholars a series of word vector models on two corpora of Early Modern Latin texts:
  * Noscemus Digital Sourcebook (a corpus of digitized Early modern scientific texts in Latin, https://doi.org/10.5281/zenodo.15040256)
  * EMLAP (a corpus of digitized Early Modern Latin Alchemical Prints, https://doi.org/10.5281/zenodo.14765294)
  In addition to that, for comparison, we also implement two other word embedding models based on LASLA and OperaMaiora publicly available from here: https://embeddings.lila-erc.eu/#topnav
  In total, we offer 4 temporal models based on NOSCEMUS, 8 discipline-specific models based on NOSCEMUS, 1 model trained on the EMLAP corpus, and two pretrained models inherited from other resources.
  * NOSCEMUS - 1501-1550
  * NOSCEMUS - 1551-1600,
  * NOSCEMUS - 1601-1650,
  * NOSCEMUS - 1651-1700,
  * NOSCEMUS - Alchemy/Chemistry
  * NOSCEMUS - Astronomy/Astrology/Cosmography
  * NOSCEMUS - Biology
  * NOSCEMUS - Geography/Cartography
  * NOSCEMUS - Mathematics
  * NOSCEMUS - Medicine
  * NOSCEMUS - Meteorology/Earth sciences
  * NOSCEMUS - Physics
  * EMLAP
  * LASLA
  * Opera Maiora
  We train the models on textual data, which we previously preprocessed and automatically morphologically annotated using scripts in the following GitHub repositories: https://github.com/CCS-ZCU/noscemus_ETF and https://github.com/CCS-ZCU/EMLAP_ETL. Thus, the training textual data have the form of automatically lemmatized and morphologically annotated Latin sentences.

  From these sentences, we first filter only for words morphologically annotated as nouns (NOUN), verbs (VERB), adjectives (ADJ), and proper names (PROPN), as these words tend to be semantically most loaded words.

  Further, we calculate raw frequencies of these words across the four subcorpora. These frequencies we employ to further reduce the size of the vocabulary, i.e., the list of words for which we generate the vectors. First, we extract 2,000 most frequent (lemmatized) words for each subcorpus. This produces a list of 6643 unique words. Second, we exclude all words appearing less than 5 times in any of the subcorpora. This reduces the vocabulary to 6,005 unique lemmata. Thus, the models can be aligned by an extensive shared vocabulary overlap.

  For the models, we employ the FastText algorithm, with the exact same parametrization as in this paper:

  Sprugnoli, R., Moretti, G., & Passarotti, M. (2020). Building and Comparing Lemma Embeddings for Latin. Classical Latin versus Thomas Aquinas. Italian Journal of Computational Linguistics, 6(1). https://doi.org/10.5281/ZENODO.4618000

  This makes our vectors directly comparable with their vectors generated for Lasla and OperaMaiora.

  The models are available in the form of one pickle file as a Python dictionary of Gensim library keyed vectors: `/data/vectors_dict_comp_v0-3.pkl`. Once you download or clone the repository, you can load them directly using the following Python code snippet:
  ```python
  with open("../data/vectors_dict_comp_v0-3.pkl", "rb") as file:
      vectors_dict = pickle.load(file)
  ```

  This repository is part of the TOME project.
This repository is part of the [TOME project](https://tome.flu.cas.cz).

# Getting started

```bash
git clone [url-of-the-git-file]
cd [name-of-the-repo]
# (recommendation: create and activate a virtual environement)
pip install -r requirements.txt
```

We reccomend to use a dedicated virtual environment for the whole project:

```bash
python3 -m venv latin_venv # or specify your own source python to replicate (e.g. python3.12 etc.)
latin_venv/bin/python -m pip install --upgrade pip
latin_venv/bin/python -m pip install -r requirements.txt
latin_venv/bin/python -m ipykernel install --user -name=noscemus_kernel # create the jupyter kernel to be used by the notebooks
echo "/latin_venv/" >> .gitignore # add the virtual_venv directory to .gitignore, to prevents its synchronization via github
```

Anytime you need to install another package, run `noscemus_venv/bin/python -m pip install <package-name>` or have the environment activated: `source noscemus_venv/bin/activate`.

Finally, go to the `scripts` directory and run the Jupyter notebooks you wish;-).

---

## Scripts

The scripts are in the `scripts` subfolder and their numbers and titles should be self-explanatory. Usually, they have the form of Jupyter notebooks.
