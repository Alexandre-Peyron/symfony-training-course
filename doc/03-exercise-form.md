#Les formulaires

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/forms.html) !

Le but de l'exercice est de créer et utiliser les formulaires dans Symfony.


###Insert

> Une commande permet de générer une formulaire depuis une entité, mais nous allons d'abord le faire à la main dans le controller
>
> ```bash
> php bin/console doctrine:generate:form
> ```

- si ce n'est pas le cas, créer une entité avec 5 types de champs différents
- créer une nouvelle action de controller avec une route du genre `myentity/new`
- créer le formulaire dans le controller et l'afficher dans le template twig

```php
$form = $this->createFormBuilder($task)
```

- dans le controller, tester la validité et la soumission du formulaire et ajouter les nouvelles données en base.
- après l'ajout en base, rediriger vers la page de l'élément nouvellement créé.


###Update

- Créer une classe de formulaire, y insérer notre formulaire existant
- mettre à jour le controller pour utiliser la classe et ne plus créer directement le form dans le controller
- ajouter une action dans le controller
- sélectionner une entité en fonction de l'ID
- afficher le formulaire avec les données de l'entité
- mettre à jour l'entité en base après soumission du formulaire


###Delete

- ajouter cette fonction, sans route, dans votre controller

```php
    /**
     * Crée un formulaire pour supprimer un entité Article
     *
     */
    private function createDeleteForm(Article $article)
    {
        //on crée un formulaire
        return $this->createFormBuilder()
            ->setAction($this->generateUrl('article_delete', array('id' => $article->getId())))
            ->setMethod('DELETE')
            ->add('delete', SubmitType::class)
            ->getForm()
        ;
    }
```

- créer un nouvelle action dans le controller, dont le nom de la route est `article_delete`
- ajouter en paramètre l'id de l'entité
- créer un `$form` grâce à la nouvelle fonction
- tester la soumission du formulaire, supprimer l'entité, rediriger vers la liste de l'entité
- Ajouter le formulaire dans la page d'une entité