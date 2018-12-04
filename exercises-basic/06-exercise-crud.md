# CRUD

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/bundles/SensioGeneratorBundle/commands/generate_doctrine_crud.html) !

Le but ici est de générer les actions de base d'affichage et d'édition d'une entité.

Une commande permet de faire ceci. 

Les options à choisir seront:
 - "annotation" pour la config
 - si on désire générer les actions d'écriture (write) : yes.
 - le prefix peut porter le nom de l'entité. Ex: /article

```bash
php bin/console make:crud
```

Voilà, c'est fini.

Un controller est apparu dans votre bundle avec 5 actions: index, show, new, edit, delete.
Ce sont les actions de bases pour toutes les entités. 

Des templates ont également été créé, ainsi qu'une classe de formulaire.

Vous pouvez voir qu'au début de votre controller un `@route` est présent, cela signifie que toutes les routes du controller commencent par ce préfix.
Ex: "/article/new", "/article/edit"