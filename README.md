# Projet : Détection de fraude bancaire

**Auteur :** Mohamed Lamine OULD BOUYA  
**Objectif :** Concevoir un modèle de classification capable d’identifier les transactions frauduleuses avec un **haut rappel** et une **bonne précision-rappel (PR-AUC)**, malgré un **déséquilibre extrême** entre transactions normales et frauduleuses.

---

## Données
- **Source :** [Kaggle - Credit Card Fraud Detection](https://www.kaggle.com/mlg-ulb/creditcardfraud)
- **Taille :** 284 807 transactions, dont seulement **0.17 %** de fraudes

---

## Stack technique
- **Langage :** Python  
- **Librairies :** `pandas`, `scikit-learn`, `imbalanced-learn`, `xgboost`, `matplotlib`, `seaborn`  

---

## Méthodologie
- **Prétraitement :**
  - Standardisation des variables
  - Gestion du déséquilibre via **SMOTE**  
- **Validation :**
  - Découpage **stratifié (80/20)** pour le train/test
  - **Cross-validation (CV) stratifiée** pour l’optimisation
- **Optimisation :**
  - **GridSearchCV** appliqué à la **Logistic Regression** (pénalités, régularisation)
  - Recherche du **seuil optimal Fβ (β=2)** pour maximiser le rappel pondéré

---

## Évaluation
- **Métriques principales :**
  - PR-AUC (*Average Precision*)  
  - ROC-AUC  
  - **Rappel**, **Précision**, **F1-score**  
  - Matrice de confusion
- **Comparaison de modèles :**
  - Logistic Regression *(baseline & optimisée)*  
  - RandomForest  
  - XGBoost
- **Critère de sélection :**
  - Meilleure balance **précision / rappel**
  - Performances évaluées sur **données test indépendantes**

---

## Sorties et artefacts
- **Figures :** courbes PR et ROC, matrices de confusion, importances des features  
- **Fichiers sauvegardés :**
  - `reports/metrics.json` — performances comparatives des modèles  
  - `reports/figures/` — figures PR, ROC, importances, matrices de confusion  
  - `train_split.csv` / `test_split.csv` — échantillons d’entraînement et de test  

---

## Résumé
Ce projet illustre la construction complète d’un pipeline de détection de fraude, de la préparation des données jusqu’à l’évaluation des modèles, en appliquant les **bonnes pratiques de Machine Learning** (validation croisée, seuil optimal, gestion du déséquilibre, export des artefacts).  
Les résultats montrent une amélioration significative du **PR-AUC** et du **rappel** grâce à l’optimisation des modèles et à l’intégration de techniques de rééchantillonnage.

---

## Résultats comparatifs

| Modèle | PR-AUC | ROC-AUC | Précision | Rappel | F1-score | Seuil |
|:--|--:|--:|--:|--:|--:|--:|
| Baseline LR | 0.7189 | 0.9721 | 0.0000 | 0.0000 | 0.0000 | 1.000 |
| LR + SMOTE (grid) | 0.7243 | 0.9710 | 0.0000 | 0.0000 | 0.0000 | 1.000 |
| RandomForest | 0.8623 | 0.9515 | 0.0000 | 0.0000 | 0.0000 | 0.163 |
| XGBoost | 0.8701 | 0.9809 | 0.0000 | 0.0000 | 0.0000 | 0.849 |