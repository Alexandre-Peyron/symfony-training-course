# Routing et controllers

Première chose à faire, comme toujours, ouvrir la [documentation](https://symfony.com/doc/current/controller.html) !

L'objectif de cet exercice est de comprendre le fonctionnement du routing, des controllers et de la création de pages.

> **Une route** : c'est le chemin/URL vers votre page.

> **Un controller** : c'est la fonction PHP qui sera exécutée lorsqu'on arrivera sur la route associée. Cette fonction doit toujours retourner un résultat, l'objet `Response` de Symfony. Cette réponse peut contenir une view (HTML), du JSON, du XML, une redirection, une erreur 404...

> **Une view** : elle correspond à l'affichage de votre page.

> **Important !** Dans le cadre du cours, gardez bien en tête que **1 route = 1 controller = 1 view**. Donc pour chaque route, pensez bien à créer une nouvelle action dans le controller et une nouvelle vue. 
Plus tard, on verra que ce n'est pas toujours le cas mais pour la compréhension au départ c'est important.


### Controller et route de base

> Nous travaillons dans le dossier **src/**. C'est ici que se trouve votre code.

Effectuez la commande suivante : 

```bash
php bin/console make:controller
```

Répondez à la question demandée, et nommez ainsi votre controller (par exemple : DefaultController).

Validez.

Deux nouveaux fichiers viennent d'être créé `src/controller/DefaultController` et `templates/default/index.html.twig`

Le controller possède déjà une route :

```
/**
 * @Route("/default", name="default")
 */
public function index()
{
    return $this->render('default/index.html.twig', [
        'controller_name' => 'DefaultController',
    ]);
}
```


Créez une première action de controller simple en ajoutant à la suite :

```php

    /**
     * @Route("/lucky/number/", name="lucky_number")  //CECI EST DU CODE !!!! C'est une annotation PHP
     *
     * Au final, cela donne l'url suivante: http://localhost:8000/lucky/number/
     *
     */
    public function numberAction()
    {
        // génération d'un nombre aléatoire
        $number = mt_rand(0, 100);
        //ici on va chercher le template et on lui transmet la variable
        return $this->render('default/number.html.twig', [
            // pour fournir des variables au template
            // a gauche, le nom qui sera utilisé dans le template
            // a droite, la valeur
            'number' => $number
       ]);
    }
   
```
Nous avons créé ici une route `@Route(/"lucky/number")` et une action de controller `numberAction()`.

Ajoutez à présent le template associé : `/templates/default/number.html.twig`

```twig
{% extends 'base.html.twig' %}

{% block body %}
    {{number}}
{% endblock %}
```

Accédez maintenant à l'URL [http://localhost:8000/lucky/number/](http://localhost:8080/lucky/number)


Maintenant, ajoutez un paramètre à l'url qui correspond au nombre max :
 
 
```php
    // [...]

    /**
     * @Route("/lucky/number/{max}", name="lucky_number")  // Ceci est toujours du code !
     *
     * exemple d'url: http://localhost:8000/lucky/number/100
     *
     */
    public function numberAction($max)
    {
        $number = mt_rand(0, $max);
        
        return $this->render('default/number.html.twig', [
            'number' => $number
        ]);
    }
    
    // [...]
```

Etape suivante, ajoutez une contrainte pour que ce paramètre soit obligatoirement un nombre. Pas de code en plus dans le controller ici, tout se fait en annotation, fouillez dans la doc pour trouver.

Dernière étape, faire en sorte que ce paramètre soit optionnel et qu'il ait une valeur par défault;
> Attention : Une fois le nombre devenu optionnel, retirez le de l'URL 
> mais pensez également à retirer le dernier "/"


### Routing avancé

Si vous ne l'aviez pas encore ouverte voici la doc concernant le [routing](https://symfony.com/doc/3.4/routing.html).

> Lors que vous créez un nouveau controller, il y a une nomenclature précise à respecter. Le nom de la fonction doit toujours être suffixée (finir) par "Action".

Créez une nouvelle action dans le `controller` avec comme route de base `/blog`.

Ajoutez 3 paramètres à l'URL: _locale, year, title.

Dans la vue `blog.html.twig`, affichez une phrase du genre: "Voici l'article $title, de l'année $year, en langue $_locale".

Ajoutez les contraintes suivantes:
- _locale ne peut être que 'fr' ou 'en'
- year doit être un nombre à 4 chiffre
- title n'est composé que de lettres, chiffres ou -

Dans la vue, si la _locale est 'en', afficher le texte en anglais.

Bonus: faire en sorte que _locale soit optionnelle et que sa valeur par défaut soit 'fr'
