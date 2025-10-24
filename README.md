# Modélisation Hybride de la Volatilité Financière (GARCH + ML)

![GitHub language count](https://img.shields.io/github/languages/count/VOTRE_NOM_UTILISATEUR/VOTRE_REPO?style=for-the-badge)
![GitHub top language](https://img.shields.io/github/languages/top/VOTRE_NOM_UTILISATEUR/VOTRE_REPO?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue.svg?style=for-the-badge)

Ce projet de recherche, mené dans le cadre du cours de Data Mining à l'École Mohammadia d'Ingénieurs, explore l'efficacité des modèles hybrides combinant la robustesse des modèles GARCH traditionnels avec la flexibilité des algorithmes de Machine Learning pour la prévision de la volatilité des actifs financiers.

---

## 📋 Table des Matières
1. [Contexte du Projet](#-contexte-du-projet)
2. [Objectif Principal](#-objectif-principal)
3. [Méthodologie](#-méthodologie)
    - [Modèles Étudiés](#modèles-étudiés)
    - [Stratégie d'Hybridation](#stratégie-dhybridation)
    - [Données et Protocole](#données-et-protocole)
4. [📊 Principales Conclusions](#-principales-conclusions)
5. [📂 Structure du Dépôt](#-structure-du-dépôt)
6. [🚀 Comment Utiliser](#-comment-utiliser)
7. [Auteurs et Remerciements](#-auteurs-et-remerciements)

---

## 🎯 Contexte du Projet

La prévision précise de la volatilité est un enjeu fondamental en finance quantitative. Si les modèles de la famille GARCH sont une référence pour capturer des faits stylisés comme le *volatility clustering*, leurs hypothèses paramétriques limitent leur capacité à modéliser des dynamiques complexes.

Ce projet se positionne à l'intersection de l'économétrie et de l'intelligence artificielle pour répondre à cette problématique, en évaluant si une approche synergique peut surpasser les méthodes traditionnelles.

## 💡 Objectif Principal

L'hypothèse centrale de ce travail est que **l'intégration des prévisions issues des modèles GARCH en tant que variables explicatives additionnelles (`features`) peut significativement améliorer la capacité prédictive des modèles de Machine Learning.**

Nous cherchons à démontrer et quantifier ce gain de performance à travers une étude empirique comparative rigoureuse.

## 🛠️ Méthodologie

### Modèles Étudiés
-   **Famille GARCH (12 variantes)** :
    -   GARCH, EGARCH, APARCH, GJR-GARCH
    -   Avec 3 distributions d'erreurs : Normale, Student-t (t), et Generalized Error Distribution (GED).
-   **Machine Learning (4 modèles)** :
    -   XGBoost
    -   Random Forest
    -   Deep Feed Forward Neural Network (DFFNN)
    -   Long Short-Term Memory (LSTM)

### Stratégie d'Hybridation
Pour chaque actif, notre approche se déroule en quatre étapes :
1.  **Ajustement GARCH** : Les 12 modèles GARCH purs sont entraînés sur les séries de rendements.
2.  **Génération de Features** : Les prédictions de volatilité de chaque modèle GARCH sont générées.
3.  **Entraînement ML de Base** : Les 4 modèles ML de base sont entraînés en utilisant uniquement les 10 derniers lags des rendements et de la volatilité réalisée comme `features`.
4.  **Construction des Modèles Hybrides (48 variantes)** : Pour chaque modèle ML de base, nous créons 12 versions hybrides en ajoutant, une par une, chacune des 12 prédictions GARCH comme une `feature` supplémentaire.

### Données et Protocole
-   **Portefeuille** : 20 actions diversifiées (AAPL, AMZN, NVDA, etc.).
-   **Période** : 1er Janvier 2010 au 31 Décembre 2023 (données de Yahoo Finance).
-   **Métrique d'Évaluation** : Root Mean Squared Error (RMSE).
-   **Protocole** : Séparation temporelle des données (80% entraînement, 20% test).

## 📊 Principales Conclusions

1.  **Domination Claire des Modèles Hybrides et ML** : Les modèles ML (purs et hybrides) surclassent systématiquement les modèles GARCH traditionnels. Pour 17 des 20 actifs (85%), le meilleur modèle global est un modèle hybride.
2.  **Gain de Performance Substantiel** : La réduction du RMSE est drastique. Par exemple, pour l'action AAPL, le meilleur modèle ML pur réduit l'erreur de 82% par rapport au meilleur modèle GARCH.
3.  **Pertinence des Features GARCH** : L'amélioration apportée par les modèles hybrides confirme que les prédictions GARCH contiennent une information précieuse et complémentaire aux `features` temporelles classiques (lags).
4.  **Efficacité des Modèles Asymétriques** : Les `features` issues des modèles GARCH asymétriques (EGARCH, GJR-GARCH, APARCH) et/ou avec des distributions à queues épaisses (t, GED) se sont révélées les plus bénéfiques.
5.  **Performance des Modèles d'Ensemble** : Les modèles basés sur les arbres de décision (Random Forest, XGBoost) ont montré une performance robuste et constante, que ce soit en version pure ou hybride.

## 📂 Structure du Dépôt
```text
.
├── notebooks/
│   ├── 1_Analyse_Comparative_NVIDIA.ipynb   # Notebook principal avec l'étude détaillée
│   └── 2_Code_Execution_Parallele.ipynb     # Script pour la parallélisation sur Colab
│
├── results/
│   ├── comparative_results.csv              # Fichiers CSV contenant les RMSE de tous les modèles
│   └── ...
│
├── .gitignore                               # Fichier pour ignorer les artefacts
└── README.md                                # Vous êtes ici !
```
## 🚀 Comment Utiliser

1.  **Cloner le dépôt :**
    ```bash
    git clone https://github.com/VOTRE_NOM_UTILISATEUR/Hybrid-Volatility-Modeling.git
    cd Hybrid-Volatility-Modeling
    ```

2.  **Installer les dépendances :**
    Il est recommandé d'utiliser un environnement virtuel.
    ```bash
    pip install -r requirements.txt
    ```
    *(Note : un fichier `requirements.txt` serait un excellent ajout à votre projet !)*

3.  **Explorer les résultats :**
    -   Ouvrez les notebooks dans le dossier `/notebooks` pour suivre la méthodologie pas à pas.
    -   Consultez les fichiers CSV dans le dossier `/results` pour une vue d'ensemble de toutes les performances.

## ✍️ Auteurs et Remerciements

Ce projet a été réalisé par :
-   **Atou El Yazid**
-   **Houbbadi Abderrahim**
-   **Serroukh Haitam**

Nous tenons à remercier notre encadrant, le **Professeur Lamrani Youssef**, pour sa direction éclairée et ses précieux conseils tout au long de ce travail.
