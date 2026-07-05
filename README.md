# Projet Machine Learning — COVID-19 🦠

Projet d'analyse et de modélisation prédictive autour de données médicales liées au COVID-19, réalisé dans le cadre de mes travaux personnels en Machine Learning.

## 🎯 Objectif du projet

Développer un modèle capable de prédire le résultat du test SARS-CoV-2 (`SARS-Cov-2 exam result`) à partir de données cliniques (tests sanguins, tests viraux, âge, etc.), en s'appuyant sur une démarche rigoureuse d'exploration puis de modélisation.

## 📁 Structure du dépôt

```
├── Exploratory_DATA_ANALYSIS.ipynb   # Analyse exploratoire des données (EDA)
├── pre-processing.ipynb              # Nettoyage et préparation des données
├── Modelisation.ipynb                # Construction et évaluation des modèles
└── README.md
```

## 1️⃣ Exploratory Data Analysis (EDA)

**Objectif :** comprendre au mieux les données avant de se lancer dans la modélisation, et poser une première stratégie ("un petit pas en avant vaut mieux qu'un grand pas en arrière").

### Analyse de forme

- **Variable cible (target)** : `SARS-Cov-2 exam result`
- **Dimensions** : 5644 lignes × 111 colonnes
- **Types de variables** : 70 qualitatives / 41 quantitatives
- **Valeurs manquantes** :
  - Beaucoup de NaN (la moitié des variables ont plus de 90% de valeurs manquantes)
  - 2 grands groupes de données identifiés : tests viraux (76% de remplissage) et taux sanguins (89% de remplissage)

### Analyse de fond

**Visualisation de la target**
- ~10% de cas positifs (558 / 5000)

**Signification des variables**
- Variables continues standardisées et asymétriques (skewed) pour les tests sanguins
- `age quantile` difficile à interpréter : les données semblent transformées mathématiquement (pas de documentation officielle sur cette transformation)
- Variables qualitatives majoritairement binaires (0/1) ; le Rhinovirus/Enterovirus ressort comme très présent parmi les tests viraux

**Relation Variables / Target**
- **Target / taux sanguins** : les taux de Monocytes, Platelets et Leukocytes semblent liés au COVID-19 → hypothèse à tester
- **Target / âge** : les individus jeunes semblent peu contaminés, mais on ne connaît ni l'âge réel ni la période exacte du dataset → prudence sur cette interprétation, à croiser avec les tests sanguins
- **Target / tests viraux** : les doubles infections sont rares (Rhinovirus/Enterovirus positif + COVID-19 négatif) → hypothèse à creuser, sans lien de causalité évident

### Analyse plus détaillée

**Relation Variables / Variables**
- Certaines variables sanguines sont très corrélées entre elles (+0.9) → point de vigilance pour la modélisation (multicolinéarité)
- Très faible corrélation entre âge et taux sanguins
- Le test rapide Influenza donne des résultats peu fiables → candidat à l'exclusion
- Les taux sanguins diffèrent entre patients malades et patients COVID-19
- La relation hospitalisation / taux sanguins est intéressante pour une potentielle prédiction du service d'affectation d'un patient

**Analyse des NaN**
- Groupe tests viraux : 1350 lignes (92% rempli / 8% manquant)
- Groupe taux sanguins : 600 lignes (87% rempli / 13% manquant)
- Intersection des deux groupes : 90 lignes

### Hypothèses à tester (H0)

- H0 : les taux sanguins des patients positifs au COVID-19 sont significativement différents de ceux des patients négatifs
- H0 : l'âge n'a pas d'effet significatif sur le résultat du test COVID-19 une fois les taux sanguins pris en compte

## 2️⃣ Pre-processing

Nettoyage et préparation des données en amont de la modélisation (gestion des valeurs manquantes, encodage des variables qualitatives, sélection des variables pertinentes en fonction de l'EDA).

## 3️⃣ Modélisation

Construction et évaluation de modèles de Machine Learning pour la prédiction du résultat du test COVID-19.

## 🛠️ Stack technique

- Python
- Pandas / NumPy
- Matplotlib / Seaborn
- Scikit-learn

## 🚀 Utilisation

```bash
git clone https://github.com/lutherkingcp0/project_Machine_Learning_covid19.git
cd project_Machine_Learning_covid19
jupyter notebook
```

Exécuter les notebooks dans l'ordre : `Exploratory_DATA_ANALYSIS.ipynb` → `pre-processing.ipynb` → `Modelisation.ipynb`

## 👤 Auteur

**AGBOSSOUMONDE Kossi Martin Luther**
