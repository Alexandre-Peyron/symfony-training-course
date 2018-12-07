# Création des entités

Je vous conseille maintenant de vous pencher sur la création et la configuration de vos entités.

> Par convention, en nomme les entités en anglais et au singulier

Vous pouvez créer un nouveau Bundle `AdminMonProjectThemeUnTrucBundle` qui va centraliser toutes ces entités.

Utilisez l'outil de création d'entités

```bash
php bin/console make:entity --regenerate Namespace/Entity

```
Créez ainsi vos entités `Article/Product`, `Category`, `Tag`...

Mettez à jour votre BDD

```bash
php bin/console doctrine:schema:update --dump-sql --force
```

Travaillez maintenant sur la gestion des relations (One-to-One, Many-to-Many...) et remettez à jour votre BDD.

Lorsque tout ça est fini. Générez votre admin avec le CRUD.
Préfixez les URLs par /admin

Voilà, vous avez une partie admin fonctionnelle et sécurisée.

