
<img width="127" alt="image2" src="https://github.com/user-attachments/assets/7c35f01a-45a5-452f-b88c-2a9a6037ee53" />

# Initiation aux biostatistiques avec R 

Cette formation d'une journée vise à vous transmettre les fondamentaux en bioinformatique nécessaires à la réalisation d'analyses statistiques dans le cadre de vos recherches et notamment de votre thèse de médecine ou de votre mémoire.

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
Nous allons travailler sur des données cliniques issues de patients adultes et pédiatriques pris en charge pour une leucémie aiguë et générés aléatoirement. 
Vous devez télécharger ce dossier en cliquant sur le lien suivant : 

[Biostat_DES_pédiatrie_2025.zip](https://github.com/user-attachments/files/21994926/Biostat_DES_pediatrie_2025.zip)

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

---
## Liens utiles

 - [Analyse R : un site très complet et didactique si vous souhaitez aller plus loin dans les analyses statistiques sous R :([https://larmarange.github.io/analyse-R/]). Un pdf regroupant l'ensemble des infos est également disponible : ([https://larmarange.github.io/analyse-R/analyse-R.pdf]) 
 - [STHDA : un site également très bien fait pour ceux qui veulent aller plus loin :([https://www.sthda.com/french/])

---

# Première Partie : Importer vos données 
Nous allons commencer par crééer puis importer un fichier au format CSV.
Le CSV est le format le plus pratique pour importer des données tabulaires dans R, car il est simple, universel et léger.

## Transformer un fichier Excel en CSV avec Microsoft Excel

1. **Ouvrir le fichier Excel**  
   - Lancez Excel et ouvrez le fichier `.xlsx` ou `.xls` que vous voulez convertir.  

2. **Vérifier les données**  
   - Assurez-vous que les données sont bien organisées en lignes et colonnes.  
   - ⚠️ Un fichier CSV ne garde **qu’une seule feuille** : seule la feuille active sera exportée.  

3. **Exporter en CSV**  
   - Cliquez sur **Fichier** → **Enregistrer sous**.  
   - Choisissez l’emplacement où sauvegarder. Pour simplifier, placez ce fichier dans le même dossier que votre projet R. Cela facilitera la gestion des chemins de fichiers, puisque R utilisera le répertoire de travail actuel pour générer tous les fichiers. 
   - Dans **Type de fichier** (ou **Format**), sélectionnez :  
     - `CSV (séparateur : point-virgule) (*.csv)` → par défaut en version française.  
     - `CSV UTF-8 (séparateur : virgule) (*.csv)` → recommandé pour garder les accents et partager à l’international.  

4. **Nommer et enregistrer**  
   - Donnez un nom à votre fichier et cliquez sur **Enregistrer**.  

5. **Confirmer les messages**  
   - Excel affichera peut-être un avertissement (perte de mise en forme, formules, plusieurs feuilles, etc.).  
   - Cliquez sur **Oui** pour continuer.  

---

## Pour importer un fichier CSV :
### Il existe deux fonctions principales pour charger un fichier CSV :
```ruby
read.csv() : utilise "," comme séparateur et "." comme décimal (format anglo-saxon)
read.csv2() : utilise ";" comme séparateur et "," comme décimal (format européen)
```
<img width="883" height="72" alt="image" src="https://github.com/user-attachments/assets/8e0ea08e-6329-478a-9da3-0512f9a05318" />

Lorsque l'on importe un fichier dans R il faut lui attribuer un objet en le nommant et en utilisant le symbole "<-" 

A chaque fois que vous aller écrire le nom de l'objet (ici _fichier_clinique_) R comprendra que vous faites référence au fichier que vous avez chargé dans cet objet. 

### Vérifier que vous avez correctement importé votre fichier
Vous pouvez explorer ce que contient votre objet dans la fenêtre "Environnement" car une fois chargé il apparaitre à cet endroit.
Vous n'avez qu'à cliquer sur le nom de votre objet pour le faire apparaître dans une nouvelle fenêtre au sein de votre projet.

<img width="949" height="441" alt="image" src="https://github.com/user-attachments/assets/c0aaafe8-7db1-4bb8-ac8a-5db73cd5a10c" />

On peut également utiliser un raccourci pour charger l'objet via la commande "command + clic gauche " sur mac ou bien "ctl gauche + clic gauche " sur PC. 

Voici à quoi ressemble notre objet 'fichier_clinique' dans l'exemple 

<img width="1498" height="661" alt="image" src="https://github.com/user-attachments/assets/6ae6c9ab-662d-4ec0-bd24-769ecb40b5a6" />

Si en revanche vous avez utilisé la mauvaise fonction pour charger le fichier .csv (read.csv à la place de read.csv2 par exemple) vous verrez que votre fichier ne s'est pas correctement chargé comme dans l'exemple ci-dessous :
Vous n'aurez alors qu'à modifier votre fonction en mettant read.csv à la place de read.csv2 ou inversement et retester si votre fichier s'est correctement chargé. 
<img width="1488" height="703" alt="image" src="https://github.com/user-attachments/assets/fab8d5a2-64e4-40a2-91e3-fa421fb30a4a" />

---

# Deuxième Partie : Faire une analyse comparative avec la fonction tableby

## Utiliser la fonction tableby pour comparer 2 groupes (ou plus) 

Une des grandes force de R est la possibilité d'utiliser des fonctions qui contiennent en réalité de grandes quantités de lignes de codes condensées dans un seul mot. 

Pour résumé grâce aux fonctions générées par d'autres utilisateurs vous allez pouvoir éviter de taper de longues lignes de codes pour réaliser les analyses souhaités. 

Au final vous n'avez pas besoin d'être un bioinformaticien pour utiliser ces fonctions. 

Vous devez seulement vous assurer que la fonction sera en mesure de lire votre table clinique, raison pour laquelle il est indispensable de respecter les consignes données au début de ce tutoriel expliquant la façon de colliger et d'organiser votre table clinique. 

Une des fonction les plus utiles dans R et qui vous fera gagner un temps considérable est la fonction** tableby**.

La fonction tableby est un véritable couteau suisse pour créer des tableaux descriptifs de haute qualité, particulièrement adaptés aux publications scientifiques et aux rapports d'analyse. Elle fait partie du package **arsenal ** développé par la Mayo Clinic.

Pour utiliser cette fonction il faut donc au préalable avoir installé (une fois au moins) puis chargé (à chaque fois que vous ouvrez votre projet) la librairie Arsenal avec la fonction : library(arsenal).

### La fonction tableby se décompose comme cela : 

En premier vous devez donner un nom à la table clinique que vous allez générer en utilisant la fonction tableby (comme le fichier clinique que vous avez crééer en utilisant la fonction read.csv au début). 

Dans la fonction tableby on retrouve en 1° le groupe que vous souhaitez comparer : ici nous voulons comparer les patients traités selon un protocole Adulte vs Pédiatrique. 

<img width="834" height="322" alt="image" src="https://github.com/user-attachments/assets/fc74dd53-a16c-4532-8fd1-66c88fdaf0e8" />

Cette information est présente dans le colonne "Protocole" de notre fichier clinique donc il faut mettre le mot "Protocole" en 1° occurence. 

Si par exemple nous avions souhaité comparer les patients atteints d'une atteinte du systeme nerveux central vs les autres nous aurions mis "Atteinte_SNC" à la place de "Protocole".

Attention : il est impératif que le mot que vous mettez dans la fonction tableby soit strictement identique au titre de votre colonne. Il ne doit pas contenir d'espace ni de chiffre en première position. Si vous vous trompez même sur une majuscule la fonction ne reconnaitra pas votre colonne dans le fichier d'analyse et vous aurez un message d'erreur. 

Tout cela explique pourquoi il faut avoir des noms de colonnes simples, **sans espace**, en évitant les majuscules quand cela est possible et les chiffres mais également faire attention à tout doublon dans le nom des colonnes. 

Après le nom de la variable de comparaison que vous avez choisi vous retrouver un tilde (vague) il s'agit d'un symbole que l'on pourrait traduire par "en fonction de" cela veut dire que vous allez comparer la répartition des autres variables en fonction de votre variable d'intérêt. 

En mettant un point après le tilde on veut comparer toutes les colonnes du fichier_clinique par rapport à la variable "Protocole". 

Si par exemple vous ne souhaitez comparer qu'une seule ou deux variables par rapport au "Protocole" on remplacerait le "." par le ou les noms des colonnes à intégrer dans la comparaison : 

<img width="702" height="34" alt="image" src="https://github.com/user-attachments/assets/ef057f4f-566b-410a-9ca2-7d512579c3cf" />

Ici par exemple on ne va tester que la répartition des GB_au_diagnostic et l'âge au diagnostic par rapport à la variable "Protocole". 

### Une fois que vous avez choisi vos variables d'analyse et générer votre table_clinique il convient maintenant de la lire et de l'exporter. 

Il existe 2 façon de faire. 
La 1° consiste à générer une page HTML (format des pages internet) qui facilite la lecture de votre table d'analyse. 
Pour crééer cette page HTML il faut utiliser la fonction **write2html**. 

<img width="392" height="37" alt="image" src="https://github.com/user-attachments/assets/4dba393e-08e7-47df-9a09-e5238b0b3e8e" />

Cette fonction est simple, il suffit de placer en 1° la table_clinique que vous avez générée précédemment avec la fonction tableby suivi du nom que vous souhaitez donner à la page HTML créée, ici "table_clinique.html". 

Il faut bien mettre le nom entre guillemet et terminer par .html pour que R comprenne que vous souhaitez crééer un fichier html. 

La page html ainsi créée se trouvera dans le répertoire de votre projet R (là où vous avez mis les fichiers cliniques, le fichier .rmd...).

<img width="296" height="191" alt="image" src="https://github.com/user-attachments/assets/7df9e0ed-83c0-465c-b140-26fda4fb6bfe" />

Elle s'ouvrira dans votre navigateur internet. 
Voici ce que cela donne dans notre exemple : 

<img width="1480" height="855" alt="image" src="https://github.com/user-attachments/assets/6f1c7087-a38e-4446-b29d-eb09d438c24d" />

La 2° solution consiste à crééer directement un fichier word comprenant votre table_clinique d'analyse :

<img width="374" height="31" alt="image" src="https://github.com/user-attachments/assets/6b86f8df-97f3-4a12-8426-13d767c0b7b7" />

il faut utiliser la fonction **write2word** selon le même principe que précédemment mais en terminant le nom de votre fichier ainsi créé par .docx.

Une fois encore le fichier word créé se situera dans le répertoire de votre projet. 

<img width="296" height="214" alt="image" src="https://github.com/user-attachments/assets/d5ecb161-6f6b-4acc-ba31-3cc3e411c6fb" />

Voici ce que cela donne : 

<img width="1446" height="822" alt="image" src="https://github.com/user-attachments/assets/3d9ba3aa-a1a6-4478-b0cb-bec9d33d79b4" />

