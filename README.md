# Projet 4 : Segmentation des Clients avec RFM et K-means
*Certaines visualisations ont été omises dans les notebooks afin d'éviter de les rendre trop lourds et impossibles à uploader. Cependant, ces visualisations sont incluses dans la présentation.*

## Vue d'ensemble du projet

Ce projet a pour objectif de réaliser une segmentation des clients en utilisant la méthode d'analyse **RFM (Récence, Fréquence, Monétaire)** combinée à l'algorithme de **K-means clustering**. La segmentation des clients permet de regrouper ces derniers en fonction de leur comportement d'achat, ce qui aide les entreprises à optimiser leurs stratégies marketing, améliorer la satisfaction client, et augmenter la rentabilité globale.

Le projet consiste à analyser les données de transactions pour identifier des groupes de clients aux comportements similaires, en utilisant des techniques de machine learning pour automatiser ce processus. Les étapes incluent la préparation des données, l'ingénierie des caractéristiques avec le scoring RFM, et l'application de l'algorithme de K-means pour découvrir les segments de clients.

## Objectifs

Les principaux objectifs de ce projet sont les suivants :

1. **Préparation et Exploration des Données** :  
   - Nettoyer le jeu de données pour le rendre prêt à l'analyse.
   - Réaliser une analyse exploratoire des données (EDA) pour comprendre la structure des données et identifier des motifs dans le comportement des clients.

2. **Ingénierie des Caractéristiques avec l'Analyse RFM** :  
   - Calculer les valeurs RFM (Récence, Fréquence, Monétaire) pour chaque client en se basant sur leur historique d'achats.
   - Normaliser les données pour assurer une comparaison équitable entre les différentes caractéristiques.

3. **Segmentation des Clients avec K-means** :  
   - Appliquer l'algorithme K-means au jeu de données RFM pour identifier différents segments de clients.
   - Analyser et interpréter les clusters obtenus pour comprendre les motifs de comportement des clients.

4. **Évaluation et Visualisation des Clusters** :  
   - Utiliser des métriques comme la méthode du coude et le score silhouette pour évaluer le nombre optimal de clusters.
   - Visualiser les segments de clients pour obtenir des insights supplémentaires sur les caractéristiques de chaque groupe.

## Déroulement du projet

1. **Collecte des Données** :  
   Le jeu de données contient les transactions des clients avec des détails tels que l'identifiant client, la date de la transaction, et le montant dépensé.

2. **Nettoyage des Données** :  
   Les valeurs manquantes, les doublons, et les valeurs aberrantes sont traités pour préparer les données à l'analyse.

3. **Analyse RFM** :  
   - **Récence** : Temps écoulé depuis le dernier achat du client.
   - **Fréquence** : Nombre de fois où un client a effectué des achats.
   - **Monétaire** : Montant total dépensé par un client.
   
   Ces caractéristiques sont extraites du jeu de données puis normalisées pour la phase de clustering.

4. **K-means Clustering** :  
   L'algorithme K-means est appliqué aux données RFM. Le nombre optimal de clusters est déterminé en utilisant des techniques telles que la méthode du coude et le score silhouette.

5. **Analyse des Clusters** :  
   Chaque cluster est analysé pour identifier des caractéristiques communes, telles que les clients à forte valeur, les acheteurs peu fréquents ou les nouveaux clients. Ces insights peuvent orienter les campagnes marketing ciblées.

6. **Visualisation des Résultats** :  
   Les clusters sont visualisés à l'aide de divers graphiques (comme des graphiques en nuage de points 2D) pour mieux comprendre la distribution des segments de clients.

7. **Maintenance de l'algorithme de clustering** :  
Pour la maintenance, l’objectif était de savoir à quelle fréquence il fallait ré-entraîner le modèle. C’est à dire qu’on cherche à savoir à quel point le clustering réalisé à une       période de l’année correspond aux clustering réalisé à une autre période.
Pour cela, on va comparer les clustering de modèles entraînés sur des périodes différentes.
J’ai utilisé plusieurs fonctions pour réaliser cela, en incluant en leur sein des docstrings et des commentaires afin de respecter la convention PEP 8.
- Création de DataFrames par Période : une première fonction est utilisée pour créer des DataFrames pour différentes périodes en spécifiant les dates de début et de fin. Cela permet de filtrer les données selon les périodes d'intérêt et de les analyser séparément.
- Analyse RFM et Score Moyen de Revue par Période : une seconde fonction génère une analyse RFM ainsi que le score moyen de revue pour chaque DataFrame créé. L'analyse suit les mêmes principes que ceux décrits précédemment, permettant une comparaison cohérente des segments de clients sur différentes périodes.
- Entraînement et Comparaison des Modèles K-means :  
   Une boucle `for` est utilisée pour :
   - Créer des DataFrames mensuels à partir des données disponibles jusqu'à janvier 2018, février 2018, etc.
   - Effectuer une analyse RFM pour chaque DataFrame mensuel.
   - Entraîner un modèle K-means avec 5 clusters pour chaque période.
   - Réaliser des prédictions avec chaque modèle et comparer les résultats en utilisant l'Adjusted Rand Index (ARI).

- Évaluation des Résultats : les scores ARI des modèles K-means pour chaque période sont analysés. On observe que la similitude entre les clusters diminue au fil des mois. Il est nécessaire de définir un seuil, par exemple un score ARI inférieur à 0.50, en dessous duquel le modèle est considéré comme non pertinent et doit être réentraîne. Dans ce cas, une réévaluation tous les 6 mois peut être envisagée.

### Conclusion

En conclusion, on a pu voir comment entraîner un modèle de clustering, en optimisant les hyperparamètres et en évaluant la qualité du clustering. On a pu visualiser les cluster et les interpréter pour comprendre les profils de clients que le modèle à créer.
Pour la maintenance de l'algorithme de clustering, la similitude diminue au fur et à mesure des mois. Il faut décider d’un seuil en dessous duquel on considère que le clustering réalisé par le modèle n’est plus pertinent et doit être remis à jour. Par exemple si on considère qu’un score ARI inférieur à 0.50 est trop faible, on devrait ici ré-entraîner le modèle tous les 6 mois.


## Outils & Librairies

- **Langage de programmation** : Python
- **Librairies** :
  - `pandas`, `numpy` pour la manipulation des données
  - `sqlite3` pour la manipulation des données sql
  - `matplotlib`, `seaborn` pour la visualisation des données
  - `scikit-learn` pour les algorithmes de clustering
  - `plotly` pour les visualisations interactives
