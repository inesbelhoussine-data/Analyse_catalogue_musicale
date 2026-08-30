# 🎵 Analyse d'un catalogue musical et prévision des tendances avec Python

## 📌 Présentation du projet

Ce projet a pour objectif d'analyser les données d'une plateforme de streaming musical afin de mieux comprendre les caractéristiques de son catalogue et d'anticiper l'évolution de la présence du genre **Pop** dans les classements.

Le travail est organisé autour de deux grandes missions :

1. **Explorer le catalogue et réaliser des analyses statistiques**
2. **Construire des séries temporelles et réaliser des prévisions avec Prophet**

L'objectif final est de transformer les données disponibles en informations exploitables pour accompagner la prise de décision des équipes et des labels.

---

## 🎯 Objectifs

### Mission 1 — Analyse du catalogue

L'analyse exploratoire et statistique permet notamment de :

- nettoyer et fiabiliser les données ;
- distinguer les occurrences du catalogue des morceaux uniques ;
- analyser la distribution des principales caractéristiques musicales ;
- identifier et étudier les valeurs atypiques ;
- analyser les artistes et les morceaux les plus populaires ;
- étudier les relations entre différentes caractéristiques du catalogue ;
- sélectionner des tests statistiques adaptés aux données.

Trois questions statistiques principales ont été étudiées :

- Existe-t-il une association entre **Energy** et **Loudness** ?
- La **Popularity** varie-t-elle selon le **genre musical** ?
- Existe-t-il une association entre le **genre musical** et le caractère **Explicit** d'un morceau ?

---

### Mission 2 — Séries temporelles et prévision

La seconde partie du projet consiste à étudier l'évolution temporelle de la présence du genre **Pop** dans le Top 200 Global.

Le travail comprend notamment :

- la construction d'une série temporelle quotidienne ;
- le diagnostic des jours manquants ;
- la distinction entre un **vrai zéro** et un **trou de collecte** ;
- l'utilisation d'une moyenne mobile pour visualiser la tendance ;
- la séparation chronologique entre données d'entraînement et données de test ;
- l'entraînement et l'évaluation d'un modèle **Prophet** ;
- l'analyse des erreurs de prévision avec **MAE, RMSE et MAPE** ;
- la production d'une prévision à environ **6 mois** ;
- l'analyse des limites et de l'incertitude associées aux prévisions.

Une analyse complémentaire étudie également la **cadence mensuelle des sorties de morceaux Pop** à partir des dates de sortie.

---

## 🧹 Préparation et exploration des données

Le nettoyage des données comprend notamment :

- analyse des valeurs manquantes ;
- suppression des doublons stricts ;
- analyse des `track_id` apparaissant plusieurs fois ;
- conservation des informations liées aux morceaux appartenant à plusieurs genres ;
- création d'une table contenant un seul enregistrement par morceau ;
- conversion et contrôle des variables numériques ;
- analyse des valeurs atypiques à l'aide de l'IQR et des boxplots.

Plusieurs outils de statistiques descriptives sont utilisés :

- moyenne et médiane ;
- écart-type ;
- quartiles ;
- skewness ;
- kurtosis ;
- histogrammes ;
- boxplots ;
- Q-Q plots.

---

## 📊 Tests statistiques

### Energy et Loudness — Corrélation de Spearman

Les deux variables étant quantitatives et les diagnostics mettant en évidence des écarts à la normalité ainsi que des valeurs atypiques, une **corrélation de Spearman** est utilisée.

Le test permet d'étudier l'existence, le sens et la force d'une association monotone entre les deux caractéristiques.

---

### Genre et Popularity — Kruskal-Wallis

La popularité est comparée entre plusieurs groupes de genres musicaux.

Compte tenu des caractéristiques observées dans les distributions, le test non paramétrique de **Kruskal-Wallis** est utilisé.

La significativité statistique est complétée par une mesure de **taille d'effet avec epsilon carré**, afin d'évaluer l'ampleur pratique des différences observées.

---

### Genre et Explicit — Test du Chi²

Le genre musical et la variable `Explicit` étant deux variables qualitatives, leur association est étudiée à l'aide d'un **test du Chi² d'indépendance**.

Les effectifs théoriques sont contrôlés avant l'interprétation du test.

Le **V de Cramér** complète l'analyse afin d'évaluer la force de l'association observée.

---

## ⏱️ Analyse temporelle

Une série temporelle quotidienne est construite afin de représenter le :

> **nombre de morceaux Pop présents dans le Top 200 Global pour chaque journée.**

Une attention particulière est portée à la continuité de la série.

Une grille complète de dates permet notamment de distinguer :

- un **vrai zéro** : le classement est disponible mais aucun morceau Pop n'est présent ;
- un **trou de collecte** : les données du classement sont absentes pour cette date.

Une **moyenne mobile sur 30 jours** est également utilisée afin de lisser les fluctuations quotidiennes et de faciliter la lecture de la tendance générale.

---

## 🔮 Prévision avec Prophet

Le modèle **Prophet** est utilisé pour modéliser l'évolution temporelle de la présence du genre Pop.

La méthodologie respecte l'ordre chronologique des données :

1. construction de la série temporelle ;
2. séparation entre période d'entraînement et période de test ;
3. entraînement du modèle sur les données historiques ;
4. prévision de la période de test ;
5. comparaison des prévisions aux valeurs réelles ;
6. évaluation avec MAE, RMSE et MAPE ;
7. réentraînement du modèle sur l'ensemble de l'historique ;
8. prévision des 183 jours suivants.

Les prévisions sont accompagnées d'un intervalle d'incertitude afin de ne pas interpréter la trajectoire prévue comme une certitude.

---

## ⚠️ Limites

Les résultats doivent être interprétés avec prudence.

Les tests statistiques permettent d'identifier des **associations et des différences**, mais ne permettent pas à eux seuls d'établir des relations de causalité.

De même, Prophet extrapole principalement des structures observées dans l'historique. Le modèle ne peut pas anticiper parfaitement :

- un hit viral inattendu ;
- une rupture brutale de tendance ;
- un changement d'algorithme ;
- une évolution soudaine du comportement des utilisateurs ;
- d'autres événements externes absents des données historiques.

Les prévisions constituent donc avant tout un **outil d'aide à la décision**.

---

## 🛠️ Technologies et bibliothèques

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **SciPy**
- **Statsmodels**
- **Prophet**
- **Scikit-learn**
- **Jupyter Notebook**
- **Studio Visual Code**

