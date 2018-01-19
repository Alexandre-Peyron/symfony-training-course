# Utilisation de Twig

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/templating.html) !

Le but de l'exercice est de comprendre les bases de twig: héritage, inclusion, gestion des blocs. Ainsi que comment personnaliser l'affichage des éléments symfony.


#### Les bases

- Créez dans `app/Resources/views` un nouveau template `layout.html.twig` qui hérite de `base.html.twig`

```twig
{% extends 'base.html.twig' %}

{% block body %}
    {% block content %}{% endblock content %}
{% endblock body %}
```

- Toujours dans `app/Resources/views` créer 3 fichiers: `header.html.twig`, `menu.html.twig`, `footer.html.twig`.
- Ajoutez du contenu dans chaque template, exemple :

```twig
<header>Mon header</header>
```

```twig
<ul>
    <li><a href="{{ path('homepage') }}">Accueil</a></li>
    <li><a href="{{ path('lucky_number') }}">Lucky Number</a></li>
</ul>
```

```twig
<footer>Mon Footer</footer>
```

- Trouvez comment **inclure** ces 3 fichiers dans `layout.html.twig`.

- Faites hériter les pages précedemment créée (lucky number, homepage), par `{% extends 'layout.html.twig' %}`
 
 

#### Intégration

- Créez 2 fichiers dans `web/assets/`, `main.css` et `main.js`
- Dans le block **stylesheets** de `base.html.twig`, appelez le fichier css via la fonction [asset](http://symfony.com/doc/3.4/best_practices/web-assets.html)
- Positionnez votre header en haut de la page sur toute la largeur, le menu dans une colonne sur la gauche, votre contenu de page à droite et pour finir le footer en base sur toute la largeur
- Ajouter un fichier **js** dans `base.html.twig` via la fonction asset
- Si vous le souhaitez, ajoutez un framework CSS (bootstrap, foundation...)








