# CRUD

Première chose à faire, comme toujours, ouvrir la [documentation](https://symfony.com/blog/new-and-improved-generators-for-makerbundle) !

Le but ici est de générer les actions de base d'affichage et d'édition d'une entité.

Créez une nouvelle entity : 
- `Category`
    - id int
    - name String
    - description Text
    - enabled Boolean
    - created_at Datetime

Utilisez la commande suivante :   

```bash
php bin/console make:crud
```

Voilà, c'est fini.

Un controller est apparu dans votre bundle avec 5 actions: index, show, new, edit, delete.
Ce sont les actions de bases pour toutes les entités. 

Des templates ont également été créé, ainsi qu'une classe de formulaire.

Vous pouvez voir qu'au début de votre controller un `@route` est présent, cela signifie que toutes les routes du controller commencent par ce préfix.
Ex: "/article/new", "/article/edit"