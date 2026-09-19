# Projet Statistique Approfondie — Sujet 8 : Sportifs

Projet de statistiques - Analyse univariée, bivariée et tests d'hypothèses sur un jeu de données de 500 sportifs.

## Le projet

Étude d'un jeu de données de **500 sportifs** décrits par 5 variables : sexe, satisfaction, nombre de sports pratiqués, temps de réaction (ms) et temps de récupération (s). L'objectif est de caractériser ces variables par des analyses descriptives, puis de confirmer les observations à l'aide de tests statistiques adaptés.

### Nettoyage et préparation

* Import depuis `Sportifs.txt`, export en `.xlsx`
* Fonction `cleanNames` développée pour uniformiser les noms de variables (suppression des accents, remplacement des espaces/ponctuations par `_`)

### Analyse univariée

* **Variables qualitatives** (sexe, satisfaction) : tableaux de contingence, diagrammes en barres
* **Nombre de sports pratiqués** : test d'ajustement à une loi de Poisson (hypothèse rejetée, p-value = 0,49 — un résultat qui ne rejette pas H0 dans ce cas, la variable pourrait suivre une loi de Poisson)
* **Temps de réaction et de récupération** : histogrammes avec courbe de densité, droites de Henry (QQ-plots), puis **test de normalité d'Anderson-Darling** (choisi plutôt que Shapiro-Wilk ou Kolmogorov-Smirnov pour sa robustesse aux écarts en queue de distribution, adapté à l'échantillon de 500 observations) — dans les deux cas, l'hypothèse de normalité est rejetée malgré une apparence graphique trompeuse. Les paramètres sont tout de même estimés par maximum de vraisemblance (`fitdistr`) à titre indicatif

### Analyse bivariée et tests d'hypothèses

* **Pair plot** (`ggpairs`) pour une vue d'ensemble des relations entre variables
* **Corrélation de Pearson** entre temps de réaction et temps de récupération : corrélation négative forte et significative
* **Tests de Welch** (adaptation du test de Student) comparant hommes et femmes sur le temps de réaction et le temps de récupération
* **Test du χ² d'indépendance** entre sexe et satisfaction
* **Tests de Student** sur la moyenne du nombre de sports pratiqués selon le niveau de satisfaction

## Résultats principaux

* Les temps de réaction et de récupération sont **fortement corrélés négativement** : plus l'un est élevé, plus l'autre est faible
* **Différence significative selon le sexe** : les femmes ont un temps de réaction plus élevé, les hommes un temps de récupération plus élevé
* **Sexe et satisfaction ne sont pas indépendants** (test du χ², p-value < 2,2e-16)
* Le nombre de sports pratiqué diffère selon le niveau de satisfaction (les sportifs moyennement satisfaits pratiquent en moyenne plus de sports que les peu satisfaits)

## Structure du projet

* `projet sujet 8.Rmd` : script R Markdown avec l'ensemble des analyses
* `Rapport_Sujet_8.pdf` : rapport compilé
* `Sportifs.txt` / `Sportifs.xlsx` : jeu de données brutes
* `Descriptif Sportifs.pdf` : description du jeu de données

## Lancer l'analyse

1. Cloner le projet ou télécharger les fichiers
2. Installer les packages nécessaires

```r
install.packages(c("openxlsx", "dplyr", "stringr", "ggplot2", "forcats", "GGally", "MASS", "nortest"))
```

3. Ouvrir `projet sujet 8.Rmd` dans RStudio et compiler (Knit)

## Auteure

Clara GAMBARDELLO
Projet Statistiques approfondies (2024)
