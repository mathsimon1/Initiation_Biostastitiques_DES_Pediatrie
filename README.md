<img width="127" alt="image2" src="https://github.com/user-attachments/assets/7c35f01a-45a5-452f-b88c-2a9a6037ee53" />


# Initiation aux biostatistiques avec R pour les internes de pédiatrie

Cette formation d'une journée vise à vous transmettre les fondamentaux en bioinformatique nécessaires à la réalisation d'analyses cliniques dans le cadre de vos recherches et de votre thèse de médecine. 

Destinée à tous les internes de pédiatrie, elle ne présuppose aucune connaissance préalable en programmation ou en statistique. 

Notre objectif est de vous transmettre les compétences miminales pour mener à bien vos projets scientifiques et de vous donner l'assurance et l'envie de réaliser vous-mêmes vos analyses statistiques essentielles. 

R est un langage de programmation utilisé principalement dans le cadre de la recherche biomédicale. Il s'utilise via RStudio. Il s'agit d'un outil très puissant permettant de faire de statistiques mais également des figures de grande qualité que vous retrouverez dans la plupart des travaux publiés dans de grandes revues. 

Enfin, il a le mérite d'être totalement gratuit contrairement à la totalité des autres outils de statistiques que vous connaissez (GraphPad Prism, STATA, SAS...)

## Pré requis

Avant la journée de formation il est nécessaire de télécharger et installer le langage informatique que l'on va utiliser (langage R) et la plateforme sur laquelle nous allons faire tourner ce langage (RStudio). 

  ### Installer R
| Système d'exploitation | Lien téléchargement |
| :-------- | :------- |
| Windows |  https://cran.r-project.org/bin/windows/base/|
| MacOS |  https://cran.r-project.org/bin/macosx/|

  ### Installer RStudio
Une fois R correctement installé, rendez-vous sur http://www.rstudio.com/products/rstudio/download/

Choisissez bien le lien de téléchargement pour RStudio (lien n°2) ne téléchargez pas à nouveau R. 

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
- supprimer les espaces entre les mots
- harmoniser les valeurs des variables pour être cohérent (leucémie aiguë et leucémie)
- supprimer les accents et les caractères spéciaux
- remplacer les données manquantes par des cellules vides

### Télécharger le dossier 
Pour commencer à travailler sur les données nous allons utiliser les données cliniques de patients ayant été traités pour 
