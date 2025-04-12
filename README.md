<img width="127" alt="image2" src="https://github.com/user-attachments/assets/7c35f01a-45a5-452f-b88c-2a9a6037ee53" />

# Initiation aux biostatistiques avec R pour les internes de pédiatrie

Cette formation d'une journée vise à vous transmettre les fondamentaux en bioinformatique nécessaires à la réalisation d'analyses statistiques dans le cadre de vos recherches et notamment de votre thèse de médecine. 

Destinée à tous les internes de pédiatrie, elle ne présuppose aucune connaissance préalable en programmation ou en statistique. 

Notre objectif est de vous transmettre les compétences miminales pour mener à bien vos projets scientifiques afin de vous donner l'assurance et l'envie de réaliser vos analyses statistiques mais également de générer des graphiques et des courbes de survie. 

R est un langage de programmation utilisé principalement dans le cadre de la recherche biomédicale. Il s'utilise via RStudio. Il s'agit d'un outil très puissant permettant de faire des analyses statistiques mais il permet également de générer des figures de grande qualité que vous pourrez utiliser directement dans vos publications.

Enfin, il a le mérite d'être totalement gratuit contrairement aux autres logiciels de statistiques (GraphPad Prism, STATA, SAS...)

## Pré requis

Avant la journée de formation il est nécessaire de télécharger et installer le langage informatique que l'on va utiliser (langage R) et la plateforme sur laquelle nous allons utiliser ce langage de programmation (RStudio). 

RStudio sert principalement à:
- Écrire et exécuter du code R plus facilement
- Visualiser vos données et résultats dans un même endroit
- Organiser vos projets d'analyse statistique
- Créer des rapports et documents combinant texte et analyses

C'est essentiellement un environnement de travail convivial pour R, comme un logiciel tout-en-un qui rend l'analyse de données beaucoup plus simple que de travailler directement avec R dans une console basique. Comme R, il est totalement gratuit. 

  ### Installer R
| Système d'exploitation | Lien téléchargement |
| :-------- | :------- |
| Windows |  https://cran.r-project.org/bin/windows/base/|
| MacOS |  https://cran.r-project.org/bin/macosx/|

  ### Installer RStudio
Une fois R correctement installé, rendez-vous sur http://www.rstudio.com/products/rstudio/download/

Choisissez bien le lien de téléchargement pour RStudio (lien n°2) ne téléchargez pas à nouveau R. 

<img width="500" alt="install Rstudio" src="https://github.com/user-attachments/assets/272e80b7-8e0a-47ee-9d8b-c5f64df0bbf8" />


## Organisation de la journée de formation

La journée va s'organiser en deux parties. Au cours de la matinée nous verrons comment organiser le recueil des informations en vue de réaliser des analyses statistiques dans R. 

Nous verrons ensuite comment charger le fichier excel dans R afin de travailler dessus. Nous apprendrons à réaliser une table clinique correspondant à la table des caractéristiques de l'ensemble de la population globale. 

Nous verrons également comment utiliser le package "Arsenal" et la fonction tableby qui permet de comparer rapidement les différences entre deux groupes en réalisant les tests statistiques pour mettre en évidence les différences significatives en termes de caractéristiques cliniques ou biologiques. 

### L'importance de bien recueillir les données en remplissant son tableur excel
Nous reviendrons sur l'importance d'anticiper la façon dont les données seront collectées. Cette étape est primordiale pour pouvoir travailler correctement ensuite. En effet le langage de programmation informatique est très sensible aux variations et il faut d'emblée intégrer le fait que les données doivent être reportées de façon harmonisée dans le tableur excel qui servira de base à l'analyse. 

Concernant les colonnes, il faut choisir un titre:
- unique
- simple (éviter les noms de colonnes trop longs ou trop complexes). Vous pouvez ajouter un fichier excel pour expliquer les variables si elles sont trop complexes ou vous noterez les correspondances entre un chiffre et son explication
- ne commençant pas par un chiffre
- ne contenant pas d'espace entre les mots (vous pouvez utiliser l'underscore ou le tiret du bas "_" pour séparer les mots)
- sans majuscule
- sans caractères spéciaux (é, è, à, !, ? ...)

Concernant la valeur des variables : 
- elles doivent être précises (ne pas mettre de phrase)
- reproductible (si vous utilisez 1 pour "oui" vous devez garder cette notation)
- faire attention aux espaces "cachés". Ainsi si vous rentrer " 1" et "1", R va considérer 2 valeurs ; " 1" et "1" donc faites attention à ne pas mettre d'espace avant ou après la valeurs
- sans caractères spéciaux (é, è, à, !, ? ...)
- ne contenant pas d'espace entre les mots (vous pouvez utiliser l'underscore ou le tiret du bas "_" pour séparer les mots)
- en cas de données manquantes il faut laisser la case vide. Ne pas mettre ND, NA ou "données manquantes"

Exemple d'un mauvais recueil :

| Nom du patient | Age au diagnostic | ATCD | 2nd cancer 
| :-------- | :------- |:------- |:------- |
| Antoine |  13 | aucun | non
| Maxime | 10 | leucémie aiguë| oui
| Clémence | 8 | leucémie | ?
| Armand | 6 | pas d'atcd | non
| Jean | 4 | données manquantes | 1

Et la correction 

| nom | age_diagnostic | atcd | second_cancer 
| :-------- | :------- |:------- |:------- |
| antoine |  13 | aucun| 0
| maxime | 10 | leucemie_aigue| 1
| clemence | 8 | leucemie_aigue| 
| armand | 6 | aucun| 0
| jean | 4 | | 1

Dans cet exemple nous avons : 
- corriger le nom des colonnes pour éviter qu'elle ne commence par un chiffre 
- supprimer les espaces entre les mots (à la fois dans le nom des colonnes et la valeur des variables)
- harmoniser les valeurs des variables pour être cohérent ("leucémie aiguë" et "leucémie")
- supprimer les accents et les caractères spéciaux (à la fois dans le nom des colonnes et la valeur des variables)
- remplacer les données manquantes par des cellules vides

### Télécharger le dossier 
Nous allons travailler sur des données cliniques issues de patients adultes et pédiatriques pris en charge pour une leucémie aiguë. 
Vous devez télécharger ce dossier en cliquant sur le lien suivant : 
[Biostat_DES_pédiatrie.zip](https://github.com/user-attachments/files/19275319/Biostat_DES_pediatrie.zip)

Voici ce que contient ce dossier: 
- Un fichier qui correspond au projet sur le lequel nous allons travailler : **Initiation_biostat_Projet.Rproj**
  * Remarque sur le fichier projet .Rproj : Un projet dans R est une façon d'organiser votre travail qui facilite grandement la gestion de vos analyses. C'est un dossier spécial qui regroupe tous les éléments liés à une même analyse ou étude. C'est comme avoir un classeur bien organisé pour chaque étude, avec toutes les données et analyses rangées ensemble.

- Deux fichiers excel sous la forme "csv" que nous utiliserons pour travailler lors de la session : **fichier_clinique_data_survie.csv** et **fichier_clinique.csv**
  * Remarque sur les fichiers .csv : il s'agit d'une variante des fichiers excel souvent utilisée quand on fait de la bioinformatique car ils permettent de stocker un grand nombre de colonnes et de lignes avec une taille très limitée. Pour générer un fichier csv vous devez choisir cette extension au moment de sauvegarder votre fichier excel (enregistrer sous puis choisir format csv). A noter que l'on peut également charger des fichiers excel de type classiques (.xls ou .xlsx).

    Les anglo-saxons ont des fichiers csv où les colonnes sont séparées par des virgules, et les unités et décimales sont séparées par un point (utiliser **read.csv()** pour ouvrir ces fichiers. En France, on utilise un format où les colonnes sont séparées par des points-virgules, et les décimales par des virgules (utiliser **read.csv2()** pour ouvrir ces fichiers. Si vous trouvez cela obscur, c'est normal ! Nous reverrons cela pendant la journée. 

- Un fichier contenant le script de notre projet: **Initiation_biostat_script.rmd**
  * Remarque sur les script :Un script dans R est simplement un fichier texte contenant une série d'instructions ou de commandes R qui peuvent être exécutées ensemble.

    Un script est comme une recette de cuisine: une liste d'instructions à suivre dans un ordre précis pour obtenir le résultat souhaité. 

    Vous pourrez le reconnaître par son extension (.rmd)

### Ouverture du projet 
Une fois le téléchargement réalisé vous allez décompresser le fichier. 
Il faut ouvrir le fichier du projet sur lequel nous allons travailler en double-cliquant sur le fichier **Initiation_biostat_Projet.Rproj**
Rstudio se lancera automatiquement pour ouvrir votre projet. 

#### Présentation de l'environnement de travail 
Une fois que le projet est ouvert vous arriverez sur un écran vide. 
Il faut charger le script **Initiation_biostat_script.rmd** que vous trouverez en bas à droite. 

<img width="612" alt="interface" src="https://github.com/user-attachments/assets/c6cb3fa6-4bbb-49cd-ae8e-998874d5165a" />

Pour charger le script il suffit de cliquer dessus. 
Une fois que le script se charge vous devez installer les packages avec la fonction install.packages("Nom du package qui vous intéresse"). Cela vous permettra ensuite de les charger avec la fonction library("Nom du package qui vous intéresse").

**Un package** est comme une boîte à outils spécialisée pour R. Chaque package contient un ensemble de fonctions, de données et de documentation qui étendent les capacités de base de R pour réaliser des tâches spécifiques. Quand on dit **"charger une librairie"**, cela signifie activer un package pour l'utiliser dans votre session R actuelle.

<img width="612" alt="interface_V2" src="https://github.com/user-attachments/assets/3f62c331-b58b-4d52-99a0-25fd32328d1a" />

Les lignes de codes sont écrites au sein de chunk (ou "bloc de code"). Un chunk est délimité par trois guillemets (```) au début et à la fin, avec {r} juste après les premiers guillemets. 

Pour exécuter le code contenu dans un chunk il faut cliquer sur la flèche verte en haut à droite du chunk. 

Vous ne pourrez écrire du code que dans ces zones. Cela vous permet de créer des sessions dans votre script que vous pourrez exécuter de façon indépendante. 

Vous pouvez facilement insérer un chunk avec le bouton "Insert".

En exécutant le 1° chunk vous lancerez l'installation des différents packages que nous utiliserons pendant la session. 

Il est nécessaire d'avoir une connexion internet pour installer les packages. Cette installation ne doit se faire qu'une seule fois alors que le chargement des packages avec la fonction library() se fera à chaque fois en fonction des packages que vous souhaiterez utiliser dans votre projet. 

# Félicitations ! 
Si vous êtes arrivés jusqu'ici vous avez réussi à installer R et son environnement (RStudio). Vous avez téléchargé le dossier à partir duquel nous travaillerons lors de la journée de formation et vous avez peut-être même réussi à installer différents packages. 

Si ce n'est pas le cas, pas d'inquiétude nous reverrons tout cela ensemble lors de cette journée ! 

Pour toutes questions n'hésitez pas à m'envoyer un mail, je vous répondrai avec plaisir : 
**mathieu.simonin@aphp.fr**

## Liens utiles

 - [Analyse R : un site très complet et didactique si vous souhaitez aller plus loin dans les analyses statistiques sous R :([https://larmarange.github.io/analyse-R/]). Un pdf regroupant l'ensemble des infos est également disponible : ([https://larmarange.github.io/analyse-R/analyse-R.pdf]) 
 - [STHDA : un site également très bien fait pour ceux qui veulent aller plus loin :([https://www.sthda.com/french/])


<details>

<summary> Première Partie  </summary>

# Première Partie : Importer les données de recueil cliniques et crééer une table d'analyse clinique
Nous allons commencer par importer le fichier Excel au format CSV sur lequel nous allons travailler. 

Pour simplifier, placez ce fichier dans le même dossier que votre projet R. 

Cela facilitera la gestion des chemins de fichiers, puisque R utilisera le répertoire de travail actuel pour générer tous les fichiers.

## Pour importer un fichier CSV :
Il existe deux fonctions principales pour charger un fichier CSV :
```ruby
read.csv() : utilise "," comme séparateur et "." comme décimal (format anglo-saxon)
read.csv2() : utilise ";" comme séparateur et "," comme décimal (format européen)
```

</details>

<details>

<summary>Astuces pour plus tard  </summary>

### Renommer des colonnes si nécessaire
```ruby
names(donnees_cliniques)[1] <- "ID_Patient"
```

### Convertir des variables en facteurs (pour les variables catégorielles)
```
donnees_cliniques$Sexe <- factor(donnees_cliniques$Sexe)
donnees_cliniques$Groupe <- factor(donnees_cliniques$Groupe)
```

### Transformer des données numériques si besoin
```
donnees_cliniques$Age <- as.numeric(donnees_cliniques$Age)
```

## Gérer les valeurs manquantes
### Identifier les valeurs manquantes
```
colSums(is.na(donnees_cliniques))
```
### Créer un sous-ensemble sans les lignes ayant des valeurs manquantes
```
donnees_completes <- na.omit(donnees_cliniques)
```
### OU remplacer les valeurs manquantes par la moyenne (pour les variables numériques)
```
donnees_cliniques$Variable_Num[is.na(donnees_cliniques$Variable_Num)] <- mean(donnees_cliniques$Variable_Num, na.rm = TRUE)
```
<details>
