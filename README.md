# projet-fraude
# 💳 Détection de Fraude sur Transactions Bancaires

Ce projet vise à détecter automatiquement les transactions bancaires frauduleuses à partir du dataset public [Credit Card Fraud Detection (Kaggle)](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud).

---

## 📂 Structure du projet


projet-fraude/
│
├── creditcard.csv # Dataset Kaggle
├── fraude_detection.ipynb # Notebook principal
├── reports/
│ ├── metrics.json # Résultats et scores des modèles
│ └── figures/ # Visualisations exportées (PR, ROC, CM)
├── models/ # Modèles entraînés (.joblib)
├── .git/ # Suivi de version
└── README.md # Présent fichier


---

## ⚙️ Étapes du pipeline

1. **Chargement et typage mémoire léger**  
   - Conversion des variables numériques en `float32`  
   - Variable cible `Class` en `int8`

2. **EDA rapide**  
   - Distribution fortement déséquilibrée (≈ 0.17 % de fraudes).  
   - Montants très concentrés sous 500 €.  

3. **Split stratifié 80/20 (train/test)**  
   - Préserve la proportion de fraudes dans chaque échantillon.

4. **Modèles entraînés**
   - **Baseline :** Régression Logistique (données brutes, sans optimisation)  
   - **Optimisé :** Pipeline `StandardScaler + SMOTE + LogisticRegression` (GridSearchCV)
   - **Comparaison :** RandomForest & XGBoost (mêmes données, métriques homogènes)

---

## 📊 Résultats – modèle optimisé (train)

*(données extraites automatiquement depuis `reports/metrics.json`)*

| Métrique | Valeur |
|-----------|--------|
| Precision | 0.85 |
| Recall | 0.92 |
| F1-score | 0.88 |
| ROC-AUC | 0.98 |
| PR-AUC | 0.91 |
| Seuil optimal (Fβ=2) | 0.43 |

> 🔹 Ces scores reflètent le modèle **optimisé (SMOTE + GridSearch)** sur le jeu d’entraînement.  
> Les métriques sont sauvegardées dans `reports/metrics.json` et mises à jour à chaque ré-entraînement.

---

## 🧠 Comparaison des modèles (test)

| Modèle | PR-AUC | ROC-AUC | F2-score | Commentaire |
|---------|--------|----------|-----------|
| LogisticRegression (Baseline) | 0.72 | 0.95 | 0.64 | Référence brute |
| LogisticRegression + SMOTE | 0.91 | 0.98 | 0.88 | Meilleur équilibre précision/rappel |
| RandomForest | 0.90 | 0.99 | 0.87 | Stable, bon rappel |
| XGBoost | 0.93 | 0.99 | 0.89 | Léger gain global |

---

## 📈 Visualisations

Les figures associées sont disponibles dans `reports/figures/` :
- `pr_curve_train.png` — Courbe Précision-Rappel  
- `roc_curve_train.png` — Courbe ROC  
- `confusion_matrix_train.png` — Matrice de confusion  

Exemple de visualisation :
```text
.
├── reports/
│   ├── figures/
│   │   ├── pr_curve_train.png
│   │   ├── roc_curve_train.png
│   │   └── confusion_matrix_train.png

## Technologies et librairies
- Python 3.12
- Scikit-learn
- Imbalanced-learn (SMOTE)
- XGBoost
- Matplotlib / Seaborn
- Pandas / Numpy
- Joblib (export modèle)

## Exécution rapide
1️⃣ Cloner le repo
git clone https://github.com/<ton-utilisateur>/projet-fraude.git
cd projet-fraude

2️⃣ Lancer le notebook
jupyter notebook fraude_detection.ipynb

3️⃣ Regarder les résultats
Les métriques et figures se trouvent dans :
reports/metrics.json
reports/figures/


## Auteur

Projet réalisé par Mohamed Lamine OULD BOUYA (Etudiant en formation Data Scientist)
Basé sur le dataset ULB / Kaggle — Credit Card Fraud Detection (Europe, 2013)
