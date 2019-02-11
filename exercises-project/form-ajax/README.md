# Formulaire Ajax

L'objectif de cet exercice est de créer et soumettre un formulaire.

Pour cela, je vous fourni un template déjà intégré sur lequel il faut se baser : [le template](./template.zip) 

> un code soigné et parfaitement indenté sera grandement apprécié.

### Première partie

Etape par étape, il faut : 

- installer un nouveau projet Symfony.

- récupérer le template et l'intégrer dans votre projet symfony (controller et view)

> Pour les assets, pas besoin d'utiliser Webpack ou Gulp, vous pouvez mettre les fichiers css et js directement dans public.

> (BONUS) Il sera bien vu d'avoir découpé et structuré le template en base > layout > view

- créer une `entity` qui contiendra les champs de votre formulaire.

- créer le formulaire correspondant (class et view) pour ne plus avoir de formulaire en dur dans votre vue.

- faire en sorte que le formulaire puisse être soumis (manière classique pour le moment : button submit, POST, et rechargement de la page)

- les données doivent être enregistrées en BDD

- ajouter les contraintes de validation sur les champs du formulaire
    - civilité doit être 0, 1 ou -1
    - lastname est une chaine de caractères comprise entre 2 et 50 caractères.
    - firstname est une chaine de caractères comprise entre 2 et 50 caractères.
    - email doit être formater comme un email
    - téléphone est une chaine de caractères comprise entre 10 et 13 caractères, contenant des chiffres et optionnellement un + au début 
    - newsletter est un boolean pouvant être null
    
- votre formulaire doit afficher les messages d'erreur

La première partie de l'exercice est terminée. Vous vous assurez une note au dessus de la moyenne en arrivant ici, les bases de Symfony vous sont acquises.

### Deuxième partie

Pour la 2e partie, nous allons ajouter une couche de JavaScript à tout ça, pour soumettre le formualaire en Ajax.

> jQuery est inclu dans le projet, vous pouvez donc l'utiliser et/ou ajouter des plugins.

A présent, il faut :

- bloquer la validation classique du formulaire, via JavaScript (petite piste : `onSubmit` et `event.preventDefault`)

- en JS, récupérer les données du formulaire (...`serialize...) et les mettres dans une variable.

- en JS, soumettre les données du formulaire sur une action de controller spécifique.

> Pensez simple ici, ce que je vous demande n'est pas très compliqué. Si vous l'abordé de façon complexe, vous avez surement faux.

> Petite piste en js : `$.ajax`

> Petite piste côté controller SF : 
> - Pensez à désactiver le CSRF Token (l'ajax ne permet pas d'utiliser cette protection)
> - Votre controller Ajax sera très similaire au controller classique, `$form->isSubmitted` en moins
> - `new JsonResponse`...

- en cas de validation, le controller doit renvoyer 'ok' (code http 200), le JS doit afficher un message à l'utilisateur en front et reset le formulaire.

- en cas d'erreur de validation, la JsonResponse doit renvoyer la liste des erreurs de soumissions.

> L'object `$form` dans votre controller contient cette liste d'erreurs, un `dump($form)` peut être salvateur ici.

- en JS, afficher les erreurs du form

> (BONUS) Si les erreurs sont affichées sous le champ associé (et pas toutes regroupées au même endroit), cela fera des points en plus.

La 2e partie est maintenant terminée. Bravo !

### Bonus

Point bonus, faire en sorte que les messages des contraintes de validation soient inscrits dans des fichiers de traductions.


### Rendu

Le projet est à mettre sur github.
Envoyez moi ensuite le lien par email, avec nom/prénom et jusqu'où vous êtes arrivés.

Bonne continuation à tous.
