# Projet d'Analyse Macropséconomique : La Zone Euro

Ce dépôt contient l'analyse approfondie de données socio-économiques visant à explorer la pertinence de l'union monétaire européenne. Ce projet a été développé en Python (avec Pandas, Scikit-Learn et Seaborn) et suit une méthodologie rigoureuse d'analyse de données.

## 📌 Problématique

**"La zone euro est-elle une zone économique homogène ?"**

L'objectif de cette étude est d'analyser les différents agrégats économiques et les indicateurs de conditions de vie des États membres pour déterminer si la monnaie unique est appliquée sur un territoire homogène ou si, au contraire, l'Union fait face à de fortes asymétries structurelles.

---

## 🛠️ Étapes du Projet

### 1. Recherche des Données (Agrégats et Conditions de Vie)
Une base de données (`database_contries.csv`) a été constituée pour l'ensemble des pays de la zone euro, couvrant deux grandes catégories de variables :

**Agrégats Économiques :**
* PIB par habitant
* Taux de chômage
* Inflation
* Dette publique (% PIB)
* Croissance économique
* Balance commerciale

**Conditions de Vie :**
* Salaire médian
* Taux de pauvreté
* Indice de Gini (inégalités)
* Espérance de vie
* Dépenses logement (% revenu)
* Taux de privation matérielle
* IDH (Indice de Développement Humain)

---

### 2. Construction d'un Tableau Comparatif
Les données ont été chargées, nettoyées et structurées dans un DataFrame Pandas afin de constituer un tableau comparatif consolidé, assurant la cohérence de l'information pour les analyses statistiques à venir.

---

### 3. Analyse des Données et Statistiques Descriptives

#### A. Statistiques de Base (Moyenne, Médiane, Écart-Type)
La première phase analytique a consisté à calculer la moyenne, la médiane et l'écart-type pour chaque indicateur. 
Nous avons également identifié la présence d'outliers (valeurs extrêmes) grâce à des boxplots, nécessitant l'application d'une technique de *capping* (écrêtage) pour normaliser les données avant les étapes suivantes.

![Boxplots - Identification des Outliers](identificando%20outliers%20-%20boxplots.png)

#### B. Corrélation Simple
Pour comprendre comment les différentes variables économiques interagissent entre elles, nous avons calculé la corrélation de Pearson entre les variables originales et visualisé les résultats à l'aide d'une carte de chaleur (Heatmap).

![Matrice de Corrélation](matriz%20de%20correlação.png)

*Observations Clés :* Nous avons isolé de fortes corrélations (>= 0.7 ou <= -0.7), notamment entre le PIB par habitant et le salaire médian (positive forte), et entre les dépenses de logement et l'IDH (négative).

#### C. Clustering (Algorithme K-Means)
Pour répondre à la question de l'homogénéité, nous avons appliqué l'algorithme d'apprentissage non supervisé **K-Means**.
Pour déterminer le nombre optimal de groupes ($k$), nous avons utilisé la **Méthode du Coude (Elbow Method)** :

![Méthode du Coude](método%20do%20cotovelo%20-%20clusters.png)

L'inflexion claire au niveau $k=3$ nous a conduits à diviser la zone euro en trois profils macroéconomiques bien distincts.

---

### 4. Classement des Pays

Sur la base des données normalisées, nous avons classé les pays selon 3 critères synthétiques sous forme de "Scores", pour faciliter le clustering :
1. **Un classement Richesse**
2. **Un classement Stabilité Économique**
3. **Un classement Qualité de Vie**

L'algorithme K-Means a révélé la typologie suivante, visualisée par des nuages de points 2D :

**🔹 Économies à Hautes Performances (Leaders) :** Luxembourg, Irlande, Pays-Bas, Autriche, Belgique, Allemagne, Finlande, Slovénie, Estonie.
**🔹 Économies Intermédiaires (Transition) :** Lituanie, Chypre, Portugal, Malte, Slovaquie, Croatie, Lettonie, Bulgarie.
**🔹 Économies en Développement (Défis Structurels) :** France, Italie, Espagne, Grèce.

#### Visualisations des Clusters

![Clusters : Richesse vs Qualité de Vie](clusters%20-%20Riqueza%20vs%20Qualidade%20de%20Vida.png)
![Clusters : Richesse vs Stabilité Économique](clusters%20-%20Riqueza%20vs%20Estabilidade%20Econômica.png)
![Clusters : Qualité de Vie vs Stabilité](clusters%20-%20Qualidade%20de%20Vida%20vs%20Estabilidade%20Econômica.png)

---

## 🎯 Question Finale et Conclusion

**"Est-il réellement pertinent de regrouper tous ces pays dans une même union monétaire ? Les pays de la zone euro présentent-ils des caractéristiques suffisamment proches pour partager une même monnaie ?"**

### 1. Constat de l'Hétérogénéité (Réfutation de la théorie classique)
Une analyse purement objective des données indique qu'il n'est pas recommandé de regrouper ces pays. Le coefficient de variation élevé pour la dette publique (51,60%) ou le chômage (36,55%) démontre de profondes inégalités. Cela constitue une violation de la théorie classique des **Zones Monétaires Optimales (ZMO)**, développée par le prix Nobel **Robert Mundell (1961)**. 

Mundell postule que pour partager efficacement une monnaie, les économies doivent réagir de manière similaire aux chocs externes. Les données extraites du modèle K-Means prouvent catégoriquement que l'Europe est divisée en différents blocs de performance (choques asymétriques). Comme la BCE impose une politique monétaire unique, il est mathématiquement impossible d'ajuster les taux d'intérêt simultanément pour refroidir une économie surchauffée (ex: Allemagne) et stimuler une économie stagnante (ex: Grèce).

### 2. Pertinence Actuelle (L'approche Endogène)
Cependant, la pertinence réelle du bloc monétaire repose sur son interdépendance. La zone euro fonctionne selon le concept de **ZMO endogène**, théorisé par les économistes **Jeffrey Frankel et Andrew Rose (1998)**. Le partage de la monnaie force l'intégration :

* **Interdépendance structurelle :** Les économies très performantes ont besoin d'inclure des économies plus fragiles pour ancrer l'euro et éviter une appréciation excessive, garantissant la compétitivité mondiale de leurs exportations. En contrepartie, les économies instables s'abritent sous la crédibilité institutionnelle de la BCE, se protégeant des crises de change.
* **Mobilité des facteurs :** L'espace Schengen permet à la main-d'œuvre de migrer des zones stagnantes vers les zones en expansion, palliant l'absence de flexibilité des taux d'intérêt locaux.
* **Transferts fiscaux (Kenen, 1969) :** Bien qu'imparfaits, les fonds de cohésion européens simulent une redistribution centrale des richesses.

**En conclusion :** La pertinence actuelle de l'euro ne découle pas d'une similitude naturelle entre ses membres, mais plutôt de la lourde infrastructure d'intégration conçue pour atténuer les disparités. Les coûts financiers et commerciaux d'une éventuelle dissolution de la zone euro seraient aujourd'hui bien supérieurs aux charges de l'asymétrie que les données ont révélée.
