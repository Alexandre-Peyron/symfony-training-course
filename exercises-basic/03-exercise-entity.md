# Les entités

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/doctrine.html) !

Le but de l'exercice est de comprendre le fonctionnement de doctrine, des entités et des relations à la base de données.

> Doctrine est un ORM, c'est un composant complètement indépendant de Symfony

> ORM (Object Relational Mapping) : Pour faire simple, cela signifie qu'une table dans votre base de données va correspondre à une class dans votre langage de programmation (PHP, Java...) et inversement.

### Une entité

> Vous pouvez travailler directement dans AppBundle, cette fois encore.

La première chose à faire est de mettre à jour le fichier `.env` en fonction de votre environnement de développement. Notamment `DATABASE_URL=mysql://db_user:db_password@127.0.0.1:3306/db_name`.
Ensuite créez une base de données dans votre environnement local, soit manuellement, soit via la ligne de commande:
  
```bash
php bin/console doctrine:database:create
```

Nous allons maintenant créer une nouvelle entité (lisez jusqu'au bout).
Dans le cadre du cours, elle doit obligatoirement posséder les contraintes suivantes:

- avoir (au moins) un champ de type `string`
- avoir (au moins) un champ de type `text`
- avoir (au moins) un champ de type `datetime`
- avoir (au moins) un champ de type `boolean`
- avoir (au moins) un champ de type `integer`

> Lors de la création d'une entité, Symfony s'occupe automatiquement d'ajouter l'ID, vous n'avez pas besoin de le faire

> Exemple: Entity Article
> - title      | string
> - content    | text
> - created_at | datetime
> - updated_at | datetime
> - is_enabled | boolean
> - nb_like    | integer

> Il est également inutile de préfixer les champs de votre table. Ex: `article_title`, `title` suffit. Cela alourdirait votre code inutilement.

La commande pour créer une nouvelle entité est:

```bash
php bin/console make:entity

```
Le nom de l'entité se compose ainsi `MyEntity`.

Et on choisira les "annotations" pour le format.

Il faut ensuite répondre aux questions posées pour ajouter les différents champs de l'entité (Nom de l'entité, puis son type...).
Lorsque toutes les propriétés de votre entité sont ajoutées, appuyez sur "Entrer" à nouveau.

Maintenant que notre entité est créée, allez dans votre bundle, un dossier Entity a été ajouté. Il contient votre nouvelle entité.

A présent, il faut mettre à jour notre base de données.
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

> Ajoutez quelques lignes de fake données dans votre BDD pour pouvoir effectuer des tests.

Le but maintenant est de créer 2 nouvelles actions dans notre controller.
(1 route = 1 action = 1 view)

- Une action 'listArticleAction()' qui liste et affiche tous les éléments de notre nouvelle entité (findAll)
- Une action 'showArticleAction($id)' qui affiche un seul élément en fonction d'un paramètre dans l'URL (findOneBy)

L'accès à l'élément seul doit se faire depuis un clique sur un élément de la liste.
