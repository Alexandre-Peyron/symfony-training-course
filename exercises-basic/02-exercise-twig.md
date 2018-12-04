# Utilisation de Twig

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/templating.html) !

Le but de l'exercice est de comprendre les bases de twig: héritage, inclusion, gestion des blocs. Ainsi que comment personnaliser l'affichage des éléments symfony.


#### Les bases

- Créez dans `templates` un nouveau template `layout.html.twig` qui hérite de `base.html.twig`

```twig
{% extends 'base.html.twig' %}

{% block body %}
    {% block content %}{% endblock content %}
{% endblock body %}
```

- Toujours dans `templates` créer 3 fichiers: `header.html.twig`, `menu.html.twig`, `footer.html.twig`.
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
 
 

#### Intégration et WebPack-Encore

Créez 2 fichiers dans `/assets/`, `main.css` et `main.js`

Il faut à présent configurer la gestion des assets dans Symfony avec le bundle [Webpack-Encore](https://symfony.com/doc/current/frontend.html)

Dans le block **stylesheets** de `base.html.twig`, appelez le fichier css via les [méthodes du bundle](https://symfony.com/doc/current/frontend/encore/simple-example.html)

Positionnez :
 - votre header en haut de la page sur toute la largeur
 - le menu dans une colonne sur la gauche
 - votre contenu de page à droite
 - pour finir le footer en base sur toute la largeur
 
Ajouter un fichier **js** dans `base.html.twig`.

Si vous le souhaitez, ajoutez un framework CSS (bootstrap, foundation...)








