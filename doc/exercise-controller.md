#Routing et controllers

Première chose à faire, comme toujours, ouvrir la [documentation](https://symfony.com/doc/current/controller.html) !

L'objectif de cet exercice est de comprendre le fonctionnement du routing, des controllers et de la création de pages.

> Important ! Dans le cadre du cours, gardez bien en tête que 1 route = 1 controller = 1 view. Donc pour chaque route, pensez bien à créer un nouveau controller et une nouvelle vue. Ca sera un peu moins le cas en progressant mais pour la compréhension au départ c'est important.


### Controller et route de base

> Dans le cadre de l'exercice, vous pouvez travailler directement dans AppBundle

Créez un premier controller simple :

```php
namespace AppBundle\Controller;

use Symfony\Component\HttpFoundation\Response;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;

class DefaultController
{
    /**
     * @Route("/lucky/number/", name="lucky_number")  
     * au final, cela donne l'url suivante: http://localhost:8080/lucky/number
     *
     */
    public function numberAction()
    {
    
        // génération d'un nombre aléatoire
        $number = mt_rand(0, 100);
        //ici on va chercher le template et on lui transmet la variable
        return $this->render('AppBundle:Default:number.html.twig', array(
            // pour fournir des variables au template
            // a gauche, le nom qui sera utilisé dans le template
            // a droite, la valeur
            'number' => $number
        );
    }
}
```

Maintenant, ajoutez un paramètre à l'url qui correspond au nombre max :
 
 
```php

    /**
     * @Route("/lucky/number/{max}", name="lucky_number")  
     * exemple d'url: http://localhost:8080/lucky/number/100
     *
     */
    public function numberAction($max)
    {
   
        $number = mt_rand(0, $max);
        
        return $this->render('AppBundle:Default:number.html.twig', array(
            'number' => $number
        );
    }

```

Etape suivante, ajouter une contrainte pour que ce paramètre soit obligatoirement un nombre.

Dernière étape, faire en sorte que ce paramètre soit optionnel et qu'il est une valeur par défault;
