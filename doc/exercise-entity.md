# Les entités

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/doctrine.html) !

Le but de l'exercice est de comprendre le fonctionne de doctrine, des entités et des relations à la base de données.

> Vous pouvez travailler directement en AppBundle, cette fois encore.

### Une entité

La première chose à faire est de mettre à jour le fichier `app/config/parameters.yml`.
Ensuite de créer une base de données dans votre environnement local, soit manuellement, soit via la ligne de commande:
  
```bash
php bin/console doctrine:database:create
```
  

Nous allons maintenant créer une nouvelle entité, mais elle doit posséder les contraintes suivantes:

> Lors de la création d'une entité, Symfony s'occupe automatiquement d'ajouter l'ID, vous n'avez pas besoin de le faire

- avoir (au moins) un champ de type `string`
- avoir (au moins) un champ de type `text`
- avoir (au moins) un champ de type `datetime`
- avoir (au moins) un champ de type `boolean`
- avoir (au moins) un champ de type `integer`

> Exemple: Entity Article
> - title | string
> - content | text
> - created_at | datetime
> - is_enabled | boolean
> - vote | integer

La commande pour créer une nouvelle entité est:

```bash
php bin/console doctrine:generate:entity

```

Maintenant que notre entité est créée, il faut mettre à jour notre base de données.
Pour voir les requêtes à faire pour syncroniser nos entités à la BDD sont :

```bash
php bin/console doctrine:schema:update --dump-sql
```

Puis pour exécuter ces requêtes :

```bash
php bin/console doctrine:schema:update --force
```

Félicitation, votre entité est maintenant fonctionnelle.


### Dans le controller

> Ajoutez quelques lignes dans votre base de données pour pouvoir effectuer des tests.

Le but maintenant est de créer 2 nouvelles actions dans notre controller.
(1 route = 1 action = 1 view)

- Une action qui liste et affiche tous les éléments de notre nouvelle entité (findAll)
- Une action qui affiche un seul élément en fonction d'un paramètre dans l'URL (findOneBy)

L'accès à l'élément seul doit se faire depuis un clique sur un élément de la liste.

Une fois tout ceci en place, dans la liste d'éléments, créer une requête qui va lister tous les éléments et les ordonner par date.

Ensuite, ajouter un paramètre optionnel `min` dans la route pour filtrer les éléments et n'afficher que ceux dont le champ `integer` est supérieur à `min`

Dans l'exemple précédent d'entité, si `min = 10`, il faut afficher tous les articles font les votes sont supérieurs à 10.


