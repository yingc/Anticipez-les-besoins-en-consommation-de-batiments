Prédiction de la consommation d'énergie et des émissions de CO₂ de bâtiments
Projet réalisé dans le cadre de la formation Data Scientist d'OpenClassrooms (titre RNCP niveau 7).
Contexte
La ville de Seattle vise la neutralité carbone en 2050. Les relevés de consommation des bâtiments sont coûteux à obtenir. L'objectif est donc de prédire, à partir des caractéristiques d'un bâtiment non résidentiel (surface, usage, année de construction, localisation) :
sa consommation totale d'énergie ;
ses émissions de CO₂.
Le projet évalue aussi l'intérêt de l'ENERGY STAR Score, un indicateur fastidieux à calculer, pour prédire les émissions.
Données
Données publiques Seattle Building Energy Benchmarking des années 2015 et 2016 :
3 224 relevés de bâtiments non résidentiels sur les deux années ;
1 036 bâtiments conservés après nettoyage (valeurs manquantes, valeurs aberrantes, lignes incohérentes) ;
70 % des données pour l'entraînement, 30 % pour le test.
Démarche
Nettoyage : harmonisation des fichiers 2015 et 2016, filtrage des bâtiments non résidentiels, suppression des valeurs aberrantes.
Analyse exploratoire : distributions, corrélations, passage au logarithme des deux variables à prédire.
Modélisation : comparaison d'une référence naïve, de modèles linéaires (Ridge, Lasso), d'un SVR et d'un Random Forest, avec recherche des hyperparamètres par validation croisée à 5 plis.
Trois séries d'essais : consommation d'énergie, émissions de CO₂ sans l'ENERGY STAR Score, émissions de CO₂ avec ce score.
Résultats
R² sur le jeu de test (variables à prédire en logarithme) :
Variable à prédire
Ridge
Lasso
Random Forest
Consommation d'énergie
0,41
0,42
0,67
Émissions de CO₂, sans ENERGY STAR Score
0,58
0,59
0,75
Émissions de CO₂, avec ENERGY STAR Score
0,64
0,64
0,84
Le Random Forest est le meilleur modèle dans les trois cas.
L'ENERGY STAR Score améliore la prédiction des émissions (R² de 0,75 à 0,84) : il apporte une information utile.
Les variables les plus importantes sont la part d'électricité dans l'énergie utilisée, la surface totale et la surface des bâtiments.
Contenu du dépôt
Fichier
Rôle
1_notebook_exploratoire_0422.ipynb
Nettoyage et analyse exploratoire
2_notebook_prediction_0422.ipynb
Prédiction de la consommation d'énergie
3_notebook_prediction_0422.ipynb
Prédiction des émissions de CO₂ sans ENERGY STAR Score
4_notebook_prediction_0422.ipynb
Prédiction des émissions de CO₂ avec ENERGY STAR Score
Outils
Python, pandas, scikit-learn, matplotlib, seaborn.
Limites et pistes d'amélioration
L'erreur reste importante en valeur réelle (RMSE d'environ 480 tonnes de CO₂ sur le jeu de test) : le modèle sert à repérer les bâtiments les plus émetteurs, pas à estimer précisément chaque bâtiment.
Le jeu de données est petit (1 036 bâtiments) et un seul découpage entraînement/test a été utilisé.
Les parts d'électricité, de gaz et de vapeur proviennent des relevés de consommation. Un essai sans ces variables montrerait ce que le modèle peut prédire à partir des seules caractéristiques du bâtiment.
