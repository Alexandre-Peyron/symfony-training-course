# Gestion utilisateur

Dans cet exercice, nous allons installer et configurer un bundle externe qui va gérer les utilisateurs (connexion/authentification, inscription, mot de passe oublié), il s'agit de [FosUserBundle](https://symfony.com/doc/master/bundles/FOSUserBundle/index.html).

Vous pourriez tout à fait suivre la doc, mais une fois n'est pas coutume, elle est ici imcomplète.

### Prérequis

Il faut activer le système de traduction pour utiliser le bundle

```yaml
# app/config/config.yml

framework:
    translator: ~
```

### Installation

```bash
composer require friendsofsymfony/user-bundle "~2.0"
```

### Activation

Activez le bundle dans le kernel. 

Il est important d'aller du bout de la configuration avant d'essayer de charger une page. Dans le cas contraire vous aurez toujours une erreur.

```php
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new FOS\UserBundle\FOSUserBundle(),
        // ...
    );
}
```


### Créer l'entité User

Dans votre bundle, créez manuellement cette nouvelle entité.

```php
<?php
// src/AppBundle/Entity/User.php

namespace AppBundle\Entity;

use FOS\UserBundle\Model\User as BaseUser;
use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity
 * @ORM\Table(name="fos_user")
 */
class User extends BaseUser
{
    /**
     * @ORM\Id
     * @ORM\Column(type="integer")
     * @ORM\GeneratedValue(strategy="AUTO")
     */
    protected $id;

    public function __construct()
    {
        parent::__construct();
        // your own logic
    }
}
```

> IMPORTANT ! Si vous êtes attentifs, vous pouvez voir que votre class User étend de BaseUser qui provient du bundle Fos User.
Cela signifie que votre entité va hérité de toutes les propriétés (public/protected) de la classe parent.

Par défaut FosUser fourni donc :

- username	
- username_canonical | Username lowercase
- email	
- email_canonical | email lowercase
- enabled | User activé ou non
- salt | "grain de sel", utilisé pour sécuriser le mot de passe	
- password	
- last_login | date de la dernière connexion utilisateur	
- confirmation_token | token pour la confirmation par email
- password_requested_at	| utilisé pour le mot de passe oublié
- roles | roles de l'utilisateur (USER, ADMIN...)

> user est un mot réservé par SQL. Si vous voulez l'utiliser comme nom de table,
 entourez le avec des backticks, ex: @ORM\Table(name="\`user\`")
 
 ### Configurer le security.yml
 
 Vous pouvez remplacer complètement votre security.yml de base (ou commentez le # pour comparer avec celui là )
 
 ```yaml
 # app/config/security.yml
 security:
     encoders:
         FOS\UserBundle\Model\UserInterface: bcrypt  # type d'encodage pour le mot de passe
 
     role_hierarchy:
         ROLE_ADMIN:       ROLE_USER
         ROLE_SUPER_ADMIN: ROLE_ADMIN
 
     providers:
         fos_userbundle:
             id: fos_user.user_provider.username # indique à SF où aller chercher la liste des utilisateurs
 
     firewalls:
         dev: # firewall pour la barre de développement
            pattern: ^/(_(profiler|wdt)|css|images|js)/
            security: false
         main: # firewall principal
             pattern: ^/ # actif sur l'ensemble du site
             form_login:
                 provider: fos_userbundle 
                 csrf_token_generator: security.csrf.token_manager
                 # if you are using Symfony < 2.8, use the following config instead:
                 # csrf_provider: form.csrf_provider
             logout:       true
             anonymous:    true
 
     access_control: # définit les règles d'accès aux différentes parties du site
         - { path: ^/login$, role: IS_AUTHENTICATED_ANONYMOUSLY } 
         - { path: ^/register, role: IS_AUTHENTICATED_ANONYMOUSLY }
         - { path: ^/resetting, role: IS_AUTHENTICATED_ANONYMOUSLY } # autorisé pour les utilisateurs non authentifiés
         - { path: ^/admin, role: ROLE_ADMIN } # autorisé uniquement pour les utilisateur authentifiés dont le role est ROLE_ADMIN
 ```
 
 ### Configurer FosUser
 
 ```yaml
 # app/config/config.yml
 fos_user:
     db_driver: orm #doctrine
     firewall_name: main #nom du firewall créé dans security.yml
     user_class: AppBundle\Entity\User #chemin vers votre entité User
     from_email:
         address: "%mailer_user%" # variable présente dans votre parameters.yml, doit être renseigné sinon ça génère un bug
         sender_name: "%mailer_user%" # idem
 ```
 
 ### Importer les routes FosUser
 
 ```yaml
 # app/config/routing.yml
 fos_user:
     resource: "@FOSUserBundle/Resources/config/routing/all.xml"
 ```
 
 Ajoute de nouvelles routes à votre projet. Avec la commande suivante vous pouvez les voir
 
 ```bash
 php bin/console debug:router
 ```
 
 ### Mettre à jour le schéma de BDD
 
 ```bash
 php bin/console doctrine:schema:update --dump-sql --force
 ```
 
 Rendez vous sur [http://localhost:8000/login](http://localhost:8000/login) ou [http://localhost:8000/register](http://localhost:8000/register).
 
 Vous pouvez maintenant vous inscrire et vous connecter. Une fois fait, vous pouvez le vérifier dans la debug barre en bas.
 
 ### Aller plus loin
 
 On a ici simplement configurer FosUser. Le bundle permet beaucoup plus de choses, comme :
 - ajouter des propriétés à votre entité user (FirstName, LastName...)
 - [modifier le formulaire d'inscription](https://symfony.com/doc/master/bundles/FOSUserBundle/overriding_forms.html)
 - [modifier les templates](https://symfony.com/doc/master/bundles/FOSUserBundle/overriding_templates.html) 
 - [créer des utilisateurs en ligne de commande](https://symfony.com/doc/master/bundles/FOSUserBundle/command_line_tools.html)
 
 et [pleins d'autres choses](https://symfony.com/doc/master/bundles/FOSUserBundle/index.html#next-steps)
