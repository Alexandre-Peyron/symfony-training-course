# Fos User

Dans le cadre de la gestion des utilisateurs, 
on ne va pas tout recoder nous même. On va installer notre premier bundle externe: FosUserBundle.


### Installation du bundle avec composer

```bash
composer require friendsofsymfony/user-bundle "~2.0"
```

Si vous vous rendez maintenant dans composer.json, vous pouvez voir qu'une ligne a été ajouté. 
Idem dans `vendor`, un nouveau dossier FOS est apparu.


### Friend Of Symfony

Il faut maintenant configurer le bundle, tout se passe [ici](https://symfony.com/doc/master/bundles/FOSUserBundle/index.html)


Dans l'ordre, vous allez:
- activer le bundle dans `app/AppKernel.php`
- créer un nouvelle entity User qui étend du User de FOS
- modifier le `app/config/security.yml` pour appliquer les nouvelles régles d'authentification
- configurer le bundle dans `app/config/config.yml`
- ajouter les routes de FOSUserBundle
- mettre à jour le schéma de base de données

Voilà, le bundle est configuré.

Vous avez maintenant accès à une page d'inscription et de login.
