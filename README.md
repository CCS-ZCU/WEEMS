# WEEMS: Word Embeddings for Early Modern Science 

---

## Authors

* Vojtěch Kaše, Jan Tvrz, Jana Švadlenková, Petr Pavlas

## License

CC-BY-SA 4.0, see attached License.md

---

In this repository, we train a series of word vector models on Latin texts from the [Noscemus](https://wiki.uibk.ac.at/noscemus/Main_Page)) database 
of early modern scientific texts in Latin. We train the models on textual data which we previously preprocessed and 
automat morphologically annotated using scripts in the following GitHub repository: https://github.com/CCS-ZCU/noscemus_ETF.

Thus, the input data for the trained models is a set of automatically lemmatized and morphological annotated latin sentences.
From the lemmatized sentences, we filter only for words morphologically annotated as nouns (NOUN), verbs, adjectives and 







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
