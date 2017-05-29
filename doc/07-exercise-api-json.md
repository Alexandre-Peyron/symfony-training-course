# API

Le but ici est de créer un controller qui renvoie du JSON à la place de nos templates twig habituels.


# Le controller

- Créer un nouveau controller (ApiController par exemple)
- Pour la suite, on a besoin d'une entite avec 4 ou 5 types de champs, en créer une si besoin
- Maintenant, ajouter une action qui liste tous les éléments d'une entité pour l'afficher en json

```php

    use Symfony\Component\HttpFoundation\JsonResponse;

    /**
     * @Route("/api/article/all")  
     *
     */
    public function indexAction()
    {
        $data = $this->getDoctrine()
                     ->getManager()
                     ->getRepository('Bundle:Entity')
                     ->findAll();
    
        return new JsonResponse($data);
    }

```
- Admirer le résultat sur l'URL correspondante

> Pratique ! Mais pas du tout optimisé, puisque le controller renvoie toutes les infos de toutes les entités.


- Trouver le moyen pour ne renvoyer que les informations voulues


Beaucoup plus d'informations [ici](https://zestedesavoir.com/tutoriels/1280/creez-une-api-rest-avec-symfony-3/) (super source !!)

Pour approfondir, vous pouvez :
    - créer un controller qui renvoie les infos d'une seul entité
    - créer un controller pour ajouter une nouvelle ligne en base
    - créer un controller pour modifier une ligne en base
    - renvoyer des messages d'erreur en JSON avec le bon code [HTTP](https://fr.wikipedia.org/wiki/Liste_des_codes_HTTPw)


