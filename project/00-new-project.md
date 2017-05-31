# Nouveau projet

On part ici sur une base propre, je vous demanderai donc d'installer un nouveau projet via l'outil de Symfony.

Le projet sera structuré de cette manière:

* AppBundle
* Admin
  * UserBundle
  * ArticleBundle
* APIBundle


AppBundle va regrouper tout ce qui concerne l'affichage en Front

AdminUserBundle concerne la gestion des utilisateurs

AdminArticleBundle (ou un autre nom en fonction de votre thématique) va centraliser nos entités et la gestion en admin.

Cette structure est à titre indicatif, si vous pensez qu'il est judicieux 
de créer un autre bundle pour une de vos fonctionnalités (les commentaires par exemple), faites le.


Au niveau du cachier des charges, voici ce qui est demandé :

* Admin
  * créer l'entité au coeur de votre projet (Article/Product...)
  * créer une ou plusieurs entités en relation avec la première, du type `Category`, `Tag`, `Media`, `Comment`...
  * gestion en admin (index/show/new/update/delete) de ces entités
  * pour l'Article/Product, ajout d'un champ de texte riche avec CKEditor
  * pour l'Article/Product, possibilité d'upload une image
  * ajout d'une template/framework CSS en admin
  * l'admin se trouve sur /admin et est sécurisée
  
* Front
  * affichage de la liste des Article/Produit
  * affichage de la liste des Article/Produit en fonction des `Tag` et/ou `Category`
  * pour l'affichage d'un seul Article/Produit, il faut que l'URL soit `slugué` (pas d'ID dans l'url)
  * sur une page Article/Produit, possibilité de vote/like en Ajax
  * sur une page Article/Produit, possibilité de commenter
  
  
  
