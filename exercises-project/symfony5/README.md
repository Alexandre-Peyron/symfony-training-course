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
- ajoutez les fixtures correspondantes