# Commande Symfony

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/console.html) !

L'objectif de cet exercice est de créer une commande personnalisée dans Symfony pour importer des data.



### Data

Rendez-vous sur [https://www.data.gouv.fr/](https://www.data.gouv.fr/fr/) et choisissez un jeu de données (CSV ou Excel).
Téléchargez-le et placez le dans un dossier 'fixtures'.

```
app > Resources > fixtures > data
```

> On appelle fixtures, les données de base ou de test d'un projet. 
Cela peut être des données pour la BDD mais aussi des images ou des média.

### Entity

Créez une entité correspondant à vos données.
Par exemple, si vous choisissez le fichier des communes de France, votre entité sera formée ainsi :

- Nom
- Code Postal
- Numéro INSEE
- Coordonnées GPS

Une fois l'entité crée, vous pouvez passer à la création de la commande.

### Command

Le but de la commande est d'aller lire le fichier de données, et pour chaque ligne de data, créer une entité et l'enregistrer en BDD.

Vous pouvez travailler directement dans le AppBundle pour y créer un dossier `Command`. 
Créez ensuite votre classe PHP `ImportDataTownCommand.php` 


Si votre fichier de données est gros ( + de 20 000 lignes), il faut faire attention à l'optimisation. Et ne persiter les données que toutes les 20 lignes.

Afin de savoir où en est l'import, il est nécessaire de créer un preloader (ou un décompte) qui se met à jour à chaque nouvelle ligne enregistrée.


### API

Maintenant que tout est en BDD, il faut créer une API Rest pour lire ces données.


### Doc

Utilisez ce [bundle](https://github.com/nelmio/NelmioApiDocBundle) pour générer une documentation digne de ce nom.
Ainsi vos futurs utilisateurs pourront utiliser l'API facilement. 


