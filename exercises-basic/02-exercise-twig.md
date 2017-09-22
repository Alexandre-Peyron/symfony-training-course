# Utilisation de Twig

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/templating.html) !

Le but de l'exercice est de comprendre les bases de twig: héritage, inclusion, gestion des blocs. Ainsi que comment personnaliser l'affichage des éléments symfony.


#### Les bases

- Créer ou mettre à jour deux pages, pour qu'elles **héritent** de `base.html.twig`
- Dans `app/Resources/views` créer 3 fichiers: header, menu, footer.
- Dans `base.html.twig` **inclure** ces 3 fichiers.
 
 
 Pour votre culture personnelle :
- Définir ce qu'est un moteur de template.
- Pourquoi utiliser un moteur de template ?
- Citer un équivalent de Twig ?
- Quels autres framework/CMS utilisent un moteur de template ?


#### Intégration

- Ajouter un fichier **css** dans `base.html.twig` via la fonction asset
- Ajouter un fichier **js** dans `base.html.twig` via la fonction asset
- Si vous le souhaitez, ajoutez un framework CSS (bootstrap, foundation...)


#### Les Formulaires

Si ce n'est pas déjà fait, créer une page qui affiche un **formulaire** (de contact par exemple)


```twig
{{ form_start(form) }}
{{ form_widget(form) }}
{{ form_end(form) }}
```

> Ces 3 lignes permettent d'afficher un formulaire mais pas de personnaliser l'affichage

- Trouver comment **personnaliser chaque champ** de votre formulaire (la réponse se trouve [ici](http://symfony.com/doc/current/form/rendering.html) mais faites la recherche par vous même avant ;) )


#### Les boucles et conditions

Si ce n'est pas déjà fait: 
- Créer une entité si c'est pas déjà fait
- Ajouter des data dans votre BDD
- Afficher **un tableau** avec toutes les données ajoutées (boucle for)

Ensuite:
- Dans ce tableau, **une cellule sur deux**, ajouter la classe `odd`. (condition if)





