# Projet Symfony 5

Liste de tâches à effectuer pour étoffer le projet de base.

[Lien du Projet sur Github](https://github.com/Alexandre-Peyron/symfony-training-course-project-sf5)


### Clonez et installez le projet localement.

Tout est dans le [README.md](https://github.com/Alexandre-Peyron/symfony-training-course-project-sf5/blob/master/README.md) du projet.

### Compléter l'admin pour Tag et Category

L'admin est actuellement incomplète. Elle ne fonctionne bien que pour Book.

Mettez à jour les vues pour avoir le même rendu sur Tag et Category.


### Fixtures

Notre projet de base est vide et c'est plutôt rébarbatif de remplir une BDD à la main.

Utilisez l'extension [Doctrine Fixture](https://symfony.com/doc/master/bundles/DoctrineFixturesBundle/index.html) pour ajouter des données de tests.

Elles doivent contenir, dans des fichiers séparés :
- Des tags
- Des category
- Des book en relation avec Tag et Category 

### Relation One-to-One Self-referencing

Ajoutez une relation One-to-one à `Book` permettant d'avoir les tomes suivant et précédent dans une série de livres.

Dans l'ordre : 
- mettez à jour la relation
- modifiez le formulaire
- le select du formulaire ne doit pas contenir l'entité elle-même
- ajoutez les fixtures correspondantes


### Updated At

La valeur updated_at de Symfony n'est pas mise à jour.

Utilisez les [Doctrine Event](https://symfony.com/doc/current/doctrine/events.html) Symfony pour mettre à jour la valeur.

L'évènement en question est le "Pre Update".

Créer une class `App\EventListener\BookEventListener qui est un EntityListener. Déclarer la suscription au bon évènement et créez la méthode permettant de mettre à jour le updated_at.


### API Rest Simple

L'objectif ici est de créer un controller d'API pour l'entité Book.

#### GET /api/book/{id}

Vous allez commencer par la route qui permet d'afficher un livre.

Le fonctionnement est quasi le même que pour une route normale mais 2 choses diffèrent

Premièrement, la réponse. Symfony fournit une méthode permettant de renvoyer du JSON `new JsonResponse(...)`.

Deuxièmement, la sérialisation. En l'état Symfony ne sait pas transformer votre objet en JSON. Il faut utiliser pour celà le composant `serializer` de Symfony : [https://symfony.com/doc/current/serializer.html](https://symfony.com/doc/current/serializer.html)

> La sérialization est un processus complexe, je vous invite à regarder les liens suivants pour approfondir le sujet
> [https://www.novaway.fr/blog/tech/comment-utiliser-le-serializer-symfony](https://www.novaway.fr/blog/tech/comment-utiliser-le-serializer-symfony)
>
> [https://afup.org/talks/2545-maitriser-le-composant-serializer-de-symfony](https://afup.org/talks/2545-maitriser-le-composant-serializer-de-symfony)
>
> [https://openclassrooms.com/fr/courses/4087036-construisez-une-api-rest-avec-symfony/4302521-la-serialisation-avec-le-composant-serializer-de-symfony](https://openclassrooms.com/fr/courses/4087036-construisez-une-api-rest-avec-symfony/4302521-la-serialisation-avec-le-composant-serializer-de-symfony)


#### GET /api/book

Répétez ce précessus pour afficher une liste de livre.




