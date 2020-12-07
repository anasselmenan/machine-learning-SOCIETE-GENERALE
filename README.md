<h1 align="center">Machine Learning - SOCIETE GENERALE (sous Python)</h1>

## Description courte

Prédire la tendance de la production de pétrole brut sur les données de l'année précédente

## Contexte du projet

<p align="justify">L'un des principaux indicateurs du marché des ressources naturelles est la production de pétrole brut. Comprendre la variation de la production par région aide à prédire l'évolution du prix du pétrole dans ces régions et cela pour les différentes qualités du brut. Ces indicateurs peuvent être très utiles pour les équipes de Société Générale.</p>

* Prévision des revenus générés par le métier de Trade Finance 
* Mise en place d'une liste de prospection pour le front-office NAT et anticipation des besoins des clients
* <div align="justify">Ajustement des prévisions pour la charge de travail du back-office traitant les produits de financement de pétrole brut</div>

## Objectifs du challenge

<p align="justify">L'objectif de ce défi est de prédire la probabilité d'augmentation de la production de pétrole brut par trimestre par pays à partir de plusieurs indicateurs recueillis au cours de l'année précédente.</p>

## Description des données

<p align="justify">Les ensembles de données fournis contiennent des données sur le pétrole brut, y compris lease condensate à l'exclusion des NGL (hydrocarbures liquides ou liquides). Toutes les données fournies sont des Open Data provenant de "The Joint Organizations Data Initiative (JODI)". Les données historiques couvrent les déclarations de tous les producteurs de pétrole brut du monde entier pour la période allant de janvier 2002 à août 2016. Chaque ligne est définie par son identifiant unique et contient des informations historiques concernant le secteur du pétrole brut d'un pays au cours de la dernière année. Certaines de ces caractéristiques contiennent des informations agrégées sur le secteur mondial du pétrole brut. Les pays ont été anonymisés dans les données.</p>
  
<p align="justify">La séparation entre le training et le test a été faite, de sorte que les données les plus récentes ont été mises dans le jeu de données de test. L'objectif est d'estimer pour l'ensemble des données de test la probabilité de l'augmentation de la production de pétrole brut pour le trimestre suivant et cela pour chaque ligne.</p>
  
Les fichiers Train et Test contiennent les fonctions suivantes :

* **ID** : «ID» de la ligne qui contient 12 mois de données d'un pays donné et d'autres informations détaillées ci-dessus
* **month** : indice de mois, il n'y a aucune indication concernant l'année de la collecte des données
* **country** : indice des pays, les pays ont été anonymisés

Et les caractéristiques qui sont données pour chaque mois de l'année précédente :

* **closing stocks** (kmt) <div align="justify"> Niveau de stock primaire à la fin du mois dans les territoires nationaux ; comprend les stocks détenus par les importateurs, les raffineurs, les organisations boursières et les gouvernements en milliers de tonnes</div>

* **exports / imports** (kmt) <div align="justify"> Quantité de pétrole brut ayant traversé physiquement les frontières internationales, à l'exclusion du commerce de transit, des bunkers internationaux de la marine et de l'aviation en milliers de tonnes métriques</div>

* **refinery intake** (kmt) <div align="justify"> Quantité totale de pétrole observée pour entrer dans le processus de raffinage en milliers de tonnes</div>

* **WTI** (West Texas Intermediate Price) <div align="justify"> Cours de clôture du dernier jour ouvrable du mois en USD

* **SumConsing stocks**, **SumExports**, **SumImports**, **SumProduction**, **SumRefinery intake** <div align="justify"> Sommes des features précédentes sur tous les pays sur la même période en milliers de tonnes</div>

<p align="justify">Le prefix "diff" signifie que les colonnes représentent la différence entre la valeur du mois et celle du mois précédent. Le préfixe de la colonne fait référence au mois d'enregistrement. Par exemple :</p>

* **12_diffExports** est la valeur la plus proche de la tendance que nous essayons de prédire
* **1_diffExports** est la valeur la plus éloignée de la tendance que nous essayons de prédire

Un autre fichier contient la cible pour chaque «ID» des données Train. La cible est soit :

* 1 : si la production augmente pour le trimestre suivant
* 0 : si la production baisse pour le trimestre suivant

Le fichier de soumission doit être un fichier CSV au format suivant (la première ligne du fichier est l'en-tête) :

**ID**        | **Target**
------------- | -------------
ID10160       | xxxx
...           | ...
ID12159       | xxxx

xxxx est une probabilité (nombre compris entre 0 et 1 inclus), par exemple 0.5.

La métrique utilisée pour ce challenge est l'AUC (aire sous la courbe ROC).

