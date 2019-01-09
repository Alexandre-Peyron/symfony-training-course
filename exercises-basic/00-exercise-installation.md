# Installation

Première chose à faire, comme toujours, ouvrir la [documentation](https://symfony.com/doc/current/setup.html) !

L'objectif de cet exercice est d'installer et configurer un environnement de travail avec Symfony


### PHP

Pour toute la suite des exercices, il est important d'avoir PHP installé sur votre machine (via Wamp, Mamp ou autres...)
et qu'il soit accessible en variable d'environnement.

Pour tester s'il est accessible ouvrez un terminal/console et tapez:

```bash
php -v
```

Si quelque chose comme ci-dessous apparait, c'est bon !

```bash
PHP 7.1.1 (cli) (built: Feb 13 2017 10:05:49) ( NTS )
```

dans le cas contraire, il faut procéder à quelques manipulations

> Sous Windows
> 
> Allez dans Panneau de configuration puis Système et sécurité puis Sécurité/Système. Ici se trouve un bouton "Paramètre de système avancé".
> Cliquez sur variables d’environnement.
> Il vous faut maintenant ajouter le chemin d’accès vers votre exécutable PHP (php.exe) à la variable d’environnement PATH.

> Sous MacOS / Linux
>
> Normalement, PHP est déjà présent sur l'OS. Si vous utilisez un serveur local de type Mamp ou autre,
> il est possible que vous ayez 2 versions de PHP sur votre machine. Pensez à bien tout maintenir à jour 
> pour éviter les conflits.


### Symfony

Ouvrez un terminal/console et placez vous dans le futur dossier parent de votre projet.

> Dans le cas où l'infrasture réseau ne vous permettrait pas d'effectuer les actions suivantes, il un [.zip](../symfony%20download/) avec une version de Symfony 4.2

Suivez ensuite les étapes de la documentation, [*Creating Symfony Applications*](https://symfony.com/doc/current/setup.html), pour créer une nouvelle application Symfony. 
Nommez la comme vous le souhaitez (symfony-discovery par exemple). Nous travaillerons avec la dernière version stable.

Utilisez la commande suivante :

```bash
composer create-project symfony/skeleton my-project
```
Il s'agit seulement du Framework en lui-même sans l'ensemble de ses composants.

Ce n'est pas le plus pratique pour notre projet, mais c'est mieux pour la compréhension car on va devoir installer chaque composant du framework quand on en aura besoin.
On réalisera à ce moment là que le framework Symfony est en fait une multitude d'outils réunis ensemble. 
Chacun des bundles pourrait être utilisé de manière indépendante dans vos projets, même des projets sans Symfony.

Si nous voulions installer une version de Symfony "Ready to start", on utiliserait cette commande :
```bash
composer create-project symfony/website-skeleton my-project
```
La commande vous indique tous les bundles qu'elle vient d'installer. 

Via la console, placez vous maintenant dans le dossier nouvellement créé.

Tapez la commande suivante pour voir si le projet est correctement installé:

```bash
php bin/console list
```

Si la liste des commandes proposées par Symfony apparaissent, vous pouvez passer à la suite.


### Vhost

Si vous utilisez un outil de serveur local type Wamp/Mamp, configurez ici une nouvelle vhost qui pointe vers le dossier /web du projet nouvellement créé.

Je n'entre pas ici dans les détails, car cela dépend complètement de l'environnement de chacun.

Autre possibilité, Symfony possède un serveur local pour le développement, pour l'utiliser
suivez les étapes de la [documentation](http://symfony.com/doc/current/setup.html#running-the-symfony-application)




Cette première partie assez indigeste est maintenant terminée. Bravo !

Nous allons à présent examiner Symfony ensemble et mettre les mains dans le code.


  


