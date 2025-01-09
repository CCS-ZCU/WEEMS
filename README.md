# WEEMS: Word Embeddings for Early Modern Science 

---

## Authors

* Vojtěch Kaše, Jan Tvrz, Jana Švadlenková, Petr Pavlas

## License

CC-BY-SA 4.0, see attached License.md

---

In this repository, we train a series of word vector models on Latin texts from the [Noscemus](https://wiki.uibk.ac.at/noscemus/Main_Page)) database 
of early modern scientific texts in Latin. In particular, we generate models for **four Noscemus subcorpora**, each covering only works
with the date of publication falling into one of four half-centuries intervals:
* 1501-1550
* 1551-1600
* 1601-1650
* 1651-1700

We train the models on textual data which we previously preprocessed and 
automatically morphologically annotated using scripts in the following GitHub repository: https://github.com/CCS-ZCU/noscemus_ETF. 
Thus, the training textual data have the form of automatically lemmatized and morphologically annotated latin sentences.

From these sentances, we first filter only for words morphologically annotated as nouns (NOUN), verbs (VERB), 
adjectives (ADJ) and proper names (PROPN), as these words tend to be semanitically most loaded words.  

Subsequently, we calculate raw frequencies of these words across the four subcorpora. These frequencies we employ to further 
reduce the size of the vocabulary, i.e. the list of words for which we generate the vectors.   







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
