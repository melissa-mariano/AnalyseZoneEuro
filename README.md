# projet d'analyse macroéconomique : la zone euro

ce dépôt contient l'analyse approfondie de données socio-économiques visant à explorer la pertinence de l'union monétaire européenne. Ce projet a été développé en Python (avec Pandas, Scikit-Learn et Seaborn) et suit une analyse de données.

## problématique

**"la zone euro est-elle une zone économique homogène ?"**

l'objectif de cette étude est d'analyser les différents agrégats économiques et les indicateurs de conditions de vie des États membres pour déterminer si la monnaie unique est appliquée sur un territoire homogène ou si, au contraire, l'Union fait face à de fortes asymétries structurelles.

---

## 🛠️ étapes du projet

### 1. recherche des données (agrégats économiques et conditions de vie)
une base de données (`database_contries.csv`) a été constituée pour l'ensemble des pays de la zone euro, couvrant deux grandes catégories de variables :

**agrégats économiques :**
* PIB par habitant
* taux de chômage
* inflation
* dette publique (% PIB)
* croissance économique
* balance commerciale

**conditions de Vie :**
* salaire médian
* taux de pauvreté
* Indice de Gini (inégalités)
* espérance de vie
* dépenses logement (% revenu)
* taux de privation matérielle
* IDH (Indice de Développement Humain)

---

### 2. construction d'un Tableau Comparatif
les données ont été chargées, nettoyées et structurées dans un DataFrame Pandas afin de constituer un tableau comparatif consolidé, assurant la cohérence de l'information pour les analyses statistiques à venir.

---

### 3. statistiques escriptives

#### a. statistiques de base (moyenne, médiane, écart-Type)
la première phase analytique a consisté à calculer la moyenne, la médiane et l'écart-type pour chaque indicateur. 
nous avons également identifié la présence d'outliers (valeurs extrêmes) grâce à des boxplots, nécessitant l'application d'une technique de *capping* (écrêtage) pour normaliser les données avant les étapes suivantes.

![Boxplots - Identification des Outliers](imagens/identificando%20outliers%20-%20boxplots.png)

#### B. corrélation simple
pour comprendre comment les différentes variables économiques interagissent entre elles, nous avons calculé la corrélation de Pearson entre les variables originales et visualisé les résultats à l'aide d'une carte de chaleur (Heatmap).

![Matrice de Corrélation](imagens/matriz%20de%20correlação.png)

*bbservations clés :* les fortes corrélations (>= 0.7 ou <= -0.7) ont été isolé, notamment entre le PIB par habitant et le salaire médian (positive forte), et entre les dépenses de logement et l'IDH (négative).

#### C. clustering (algorithme K-Means)
pour répondre à la question de l'homogénéité, nous avons appliqué l'algorithme d'apprentissage non supervisé **K-Means**.
pour déterminer le nombre optimal de groupes ($k$), nous avons utilisé la **Méthode du Coude (Elbow Method)** :

![Méthode du Coude](imagens/método%20do%20cotovelo%20-%20clusters.png)

l'inflexion claire au niveau $k=3$ nous a conduits à diviser la zone euro en trois profils macroéconomiques bien distincts.

---

### 4. classement des pays

sur la base des données normalisées, nous avons classé les pays selon 3 critères synthétiques sous forme de "Scores", pour faciliter le clustering :
1. **Un classement Richesse**
2. **Un classement Stabilité Économique**
3. **Un classement Qualité de Vie**

l'algorithme K-Means a révélé la typologie suivante, visualisée par des nuages de points 2D :

**🔹 économies à hautes performances (leaders) :** Luxembourg, Irlande, Pays-Bas, Autriche, Belgique, Allemagne, Finlande, Slovénie, Estonie.
**🔹 économies intermédiaires (transition) :** Lituanie, Chypre, Portugal, Malte, Slovaquie, Croatie, Lettonie, Bulgarie.
**🔹 économies en développement (défis structurels) :** France, Italie, Espagne, Grèce.

#### visualisations des clusters

![Clusters Richesse vs Qualité de Vie](imagens/clusters%20-%20Riqueza%20vs%20Qualidade%20de%20Vida.png)
![Clusters Richesse vs Stabilité Économique](imagens/clusters%20-%20Riqueza%20vs%20Estabilidade%20Econômica.png)
![Clusters Qualité de Vie vs Stabilité](imagens/clusters%20-%20Qualidade%20de%20Vida%20vs%20Estabilidade%20Econômica.png)

---

## question finale et conclusion

**"est-il réellement pertinent de regrouper tous ces pays dans une même union monétaire ? Les pays de la zone euro présentent-ils des caractéristiques suffisamment proches pour partager une même monnaie ?"**

### 1. constat de l'hétérogénéité (réfutation de la théorie classique)
une analyse purement objective des données indique qu'il n'est pas recommandé de regrouper ces pays. Le coefficient de variation élevé pour la dette publique (51,60%) ou le chômage (36,55%) démontre de profondes inégalités. Cela constitue une violation de la théorie classique des **Zones Monétaires Optimales (ZMO)**, développée par le prix Nobel **Robert Mundell (1961)**. 

Mundell postule que pour partager efficacement une monnaie, les économies doivent réagir de manière similaire aux chocs externes. Les données extraites du modèle K-Means prouvent catégoriquement que l'Europe est divisée en différents blocs de performance (choques asymétriques). Comme la BCE impose une politique monétaire unique, il est mathématiquement impossible d'ajuster les taux d'intérêt simultanément pour refroidir une économie surchauffée (ex: Allemagne) et stimuler une économie stagnante (ex: Grèce).

### 2. pertinence actuelle (l'approche Endogène)
cependant, la pertinence réelle du bloc monétaire repose sur son interdépendance. La zone euro fonctionne selon le concept de **ZMO endogène**, théorisé par les économistes **Jeffrey Frankel et Andrew Rose (1998)**. Le partage de la monnaie force l'intégration :

* **interdépendance structurelle :** les économies très performantes ont besoin d'inclure des économies plus fragiles pour ancrer l'euro et éviter une appréciation excessive, garantissant la compétitivité mondiale de leurs exportations. En contrepartie, les économies instables s'abritent sous la crédibilité institutionnelle de la BCE, se protégeant des crises de change.
* **mobilité des facteurs :** l'espace Schengen permet à la main-d'œuvre de migrer des zones stagnantes vers les zones en expansion, palliant l'absence de flexibilité des taux d'intérêt locaux.
* **transferts fiscaux (Kenen, 1969) :** bien qu'imparfaits, les fonds de cohésion européens simulent une redistribution centrale des richesses.

**en conclusion :** la pertinence actuelle de l'euro ne découle pas d'une similitude naturelle entre ses membres, mais plutôt de la lourde infrastructure d'intégration conçue pour atténuer les disparités. Les coûts financiers et commerciaux d'une éventuelle dissolution de la zone euro seraient aujourd'hui bien supérieurs aux charges de l'asymétrie que les données ont révélée.
