# Les formulaires

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/forms.html) !

Le but de l'exercice est de créer et utiliser les formulaires dans Symfony.


### Insert

- si ce n'est pas le cas, créez une entité avec 5 types de champs différents
- ajoutez une action de controller avec une route du genre `myentity/new`
- [créer le formulaire](http://symfony.com/doc/current/forms.html#building-the-form) dans le controller et affichez le dans le template

```php
use Symfony\Component\Form\Extension\Core\Type\TextType;

$myEntity = new MyEntity();

$form = $this->createFormBuilder($myEntity)
    ->add('title', TextType::class)
//[...]

```

- dans le controller, testez la validité et la soumission du formulaire et ajoutez les nouvelles données en base.
- après l'ajout en base, redirigez vers la page de l'élément nouvellement créé.

```php
//[...]

$form->handleRequest($request);

if ($form->isSubmitted() && $form->isValid()) {
    $em = $this->getDoctrine()->getManager();
    $em->persist($article);
    $em->flush();

    return $this->redirectToRoute('article_show', array('id' => $article->getId()));
}

//[...]

```


> Une commande permet de générer une class de formulaire depuis une entité, dans MyBundle/Form/MyEntityType.php
>
> ```bash
> php bin/console make:form
> ```


### Update

- Créer une classe de formulaire avec la commande indiquée ci-dessus
- mettre à jour le controller pour utiliser la classe et ne plus créer directement le form dans le controller
- ajouter une action dans le controller `myentity/update`
- sélectionner une entité en fonction de l'ID
- afficher le formulaire prérempli avec les données de l'entité
- comme précédemment, tester la validité et la soumission du formulaire
- mettre à jour l'entité en base après soumission


### Delete

- ajouter cette fonction, sans route, dans votre controller

```php
    /**
     * Crée un formulaire pour supprimer un Article
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
