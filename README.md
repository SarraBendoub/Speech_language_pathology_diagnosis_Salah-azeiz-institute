# 🎙️ Détection de la dysphonie à partir de la voix

> *Speech-language pathology diagnosis*
> Classification de voix saines et dysphoniques à partir d'enregistrements de voyelles tenues.
> Projet de fin de première année d'ingénieur, mené pour l'**Institut Salah Azaïez de Tunis**.

---

## 🎯 Le problème

En Tunisie, diagnostiquer une dysphonie demande de longues séances. Et une fois le diagnostic
posé, mesurer l'amélioration d'un patient reste difficile à objectiver : l'évaluation repose
largement sur l'oreille du praticien.

L'idée de ce projet est d'extraire des **indicateurs mesurables** à partir d'un enregistrement
simple, une voyelle tenue de deux à trois secondes, pour donner au praticien un repère chiffré
qu'il peut comparer d'une séance à l'autre.

---

## 📊 Les données

**Saarbruecken Voice Database** (Institut de phonétique, Université de la Sarre), librement
consultable en ligne : <https://stimmdb.coli.uni-saarland.de/>

Les enregistrements retenus sont les voyelles tenues **/a/**, **/i/** et **/u/**, pour des voix
saines et dysphoniques, hommes et femmes, à trois hauteurs de voix (basse, normale, haute).

> ⚠️ Les fichiers audio ne sont pas redistribués ici. Ils se téléchargent depuis la base
> d'origine, aux conditions de celle-ci. Les notebooks attendent un dossier `data/` organisé
> ainsi : `normal_man/`, `normal_women/`, `pathology_man/`, `pathology_women/`.

---

## 🧱 La démarche

Le projet suit la méthode **CRISP-DM**, de la compréhension du besoin jusqu'à l'évaluation.

| Étape | Ce qui est fait |
|---|---|
| **Préparation** | Construction d'un jeu unifié à partir de fichiers épars : nom du fichier, durée, fréquence d'échantillonnage, signal chargé, voyelle, hauteur, genre, classe |
| **Exploration** | Distributions par voyelle, hauteur et genre, boîtes à moustaches des durées, spectres comparés d'une voix saine et d'une voix dysphonique |
| **Caractéristiques** | Coefficients **MFCC**, **centroïde spectral**, **taux de passage par zéro** : des mesures de la qualité vocale, pas du contenu parlé |
| **Classification** | **Random Forest** et **KNN**, comparés sur les mêmes données |

---

## 📈 Les résultats

| Modèle | Précision voix saines | Rappel voix saines | Précision voix pathologiques | Rappel voix pathologiques |
|---|---|---|---|---|
| **Random Forest** | **0,73** | **0,69** | **0,57** | **0,62** |
| KNN | 0,66 | 0,56 | 0,46 | 0,57 |

Random Forest l'emporte sur les deux classes.

**La limite, assumée :** les scores restent nettement plus faibles sur les voix pathologiques,
moins nombreuses dans le jeu de données. Avant tout usage clinique, c'est la première chose à
corriger, par un rééquilibrage des classes et davantage d'enregistrements pathologiques.

---

## 📂 Contenu du dépôt

```
01-preparation-donnees.ipynb       chargement des audios, construction du jeu de données, visualisation
02-caracteristiques-classification.ipynb   extraction MFCC et spectrales, entraînement, évaluation
report.pdf                          le rapport complet (40 pages, soutenu le 25/05/2024)
```

## ▶️ Reproduire

1. Télécharger les enregistrements depuis la Saarbruecken Voice Database et les ranger dans `data/`.
2. Ouvrir `01-preparation-donnees.ipynb` (Colab ou Jupyter) et exécuter les cellules pour produire le jeu de données.
3. Ouvrir `02-caracteristiques-classification.ipynb` pour l'extraction des caractéristiques et la classification.

Bibliothèques : `librosa`, `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`.

---

## 📝 Contexte

Projet de fin de première année du cycle d'ingénieur en mathématiques appliquées et modélisation,
**ENSIT**, année universitaire 2023-2024. Encadrant : M. Sabeur Abid. Soutenu le 25 mai 2024.

Portfolio : <https://sarrabendoub.github.io/ai>
