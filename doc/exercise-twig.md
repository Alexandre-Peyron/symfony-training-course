#Utilisation de Twig

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/templating.html) !

Le but de l'exercice est de comprendre les bases de twig: héritage, inclusion, gestion des blocs. Ainsi que comment personnaliser l'affichage des éléments symfony.


#### Les bases

- Créer deux pages qui **hérite** de `base.html.twig`
- Dans `base.html.twig` **inclure** 3 fichiers: 1 header, 1 footer, 1 menu. 
- Définir ce qu'est un moteur de template.
- Pourquoi utiliser un moteur de template ?
- Citer un concurrent de Twig ?
- Quels autres framework/CMS utilisent un moteur de template ?


#### Intégration

- Ajouter un fichier **css** dans `base.html.twig` via le gestionnaire d'asset
- Ajouter un fichier **js** dans `base.html.twig` via le gestionnaire d'asset
- Si vous le souhaitez, ajoutez un framework CSS (bootstrap...)


#### Les Formulaires

- Créer une page qui affiche un **formulaire** (de contact par exemple)

> Pour afficher un formulaire, il est plus pratique de créer une entité en amont, mais pas forcément nécessaire

```twig
{{ form_start(form) }}
{{ form_widget(form) }}
{{ form_end(form) }}
```

> Ces 3 lignes permettent d'afficher un formulaire mais pas de personnaliser l'affichage

- Trouver comment **personnaliser chaque champ** de votre formulaire (la réponse se trouve [ici](http://symfony.com/doc/current/form/rendering.html) mais faites la recherche par vous même avant ;) )


#### Les boucles et conditions

- Créer une entié si c'est pas déjà fait
- Ajouter des data dans votre BDD
- Afficher **un tableau** avec toutes les données ajoutés (boucle for)
- Dans ce tableau, **une cellule sur deux**, ajouter la classe `odd`. (condition if)





