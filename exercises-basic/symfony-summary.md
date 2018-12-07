# Symfony

## Globalement qu'est-ce que c'est ?

Un **framework** PHP qui fournit des outils ainsi qu'une méthodologie pour le développement de vos projets web.

On dit que Symfony est **full stack** car il propose à la fois des dispositifs front et back pour une expérérience complète.

## Liste non exhaustive de ce que fait Symfony

* Du Routing
* Génération et validation de formulaires
* Gestion des assets
* Multi-langue
* Console
* Debug
* Sécurité

Avec des outils externes on ajoute:
* ORM ([Doctrine](http://www.doctrine-project.org/)/ [Propel](http://propelorm.org/))
* Templating ([Twig](http://twig.sensiolabs.org/))
* Envoi de mail ([Swift Mailer](http://swiftmailer.org/))

## Actions de base à faire

L'utilisation de Symfony passe beaucoup par la console/terminal pour les tâches qui s'automatisent. A noter qu'après un peu de pratique vous pourrez créer vos propres commandes.

> Pour avoir la liste des commandes disponibles `php bin/console list`

### Pour installer Symfony

Se rendre sur [https://symfony.com/download](https://symfony.com/download)

>Dans notre cas, la configuration réseau de l'IUT ne permet pas d'utiliser l'installeur Symfony, un [.zip](https://github.com/Alexandre-Peyron/symfony-licence-presentation/blob/master/symfony%20download/symfony-licence-3.2.zip) est donc disponible sur ce repository


### A l'installation

Ouvrir un terminal/Console.

Première commande à faire si vous n'avez pas d'environnement local

`php bin/console server:run`

Puis se rendre sur [http://localhost:8000/](http://localhost:8000/)

> Le serveur fonctionne tant que la commande est en cours d'exécution. Donc pour utiliser d'autres commandes, il faut ouvrir un 2e terminal/console

Se rendre sur [http://localhost:8000/config.php](http://localhost:8000/config.php) pour vérifier si l'environnement local est bien configuré


### Création d'une nouvelle page

- Créer une nouvelle route en ajoutant une action à notre `controller`
- Ajouter un template

```php
namespace AppBundle\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Request;

class DefaultController extends Controller
{
    /**
     * @Route("/", name="homepage")
     */
    public function indexAction(Request $request)
    {
        //ici le template se situe dans app/Resources/views/default
        return $this->render('default/index.html.twig');
    }
    
    
    /**
     * @Route("/contact", name="page_contact")
     */
    public function contactAction(Request $request)
    {
        $number = mt_rand(0, 100);
    
        //dans ce cas, le template se situe dans src/AppBundle/Resources/views/Contact
        return $this->render('AppBundle:Contact:index.html.twig', array(
            
            //pour fournir des variables au template
            'number' => $number
        );
    }
    
}
```

> Pour tester si votre route est bien prise en compte par Symfony, vous pouvez utiliser la commande `php bin/console debug:router`


### Utilisation de la base de données

- Créer une nouvelle base de données dans son environnement local
- Mettre à jour le  fichier `.env`


### Création d'une nouvelle entité

`php bin/console make:entity`

> Une entité correspond à une table dans votre base de données.

Après création, si vous ajoutez des propriétés à votre entité, par exemple `$is_enabled`,
la commande pour mettre à jour les `Getter` et `Setter` est :

`php bin/console make:entity --regenerate Namespace/Entity`

### Pour mettre à jour la base de données

Pour afficher la liste des requêtes nécessaires pour syncroniser la BDD :

`php bin/console doctrine:schema:update --dump-sql`

Pour effectuer ces requêtes :

`php bin/console doctrine:schema:update --force`


### Utilisation de doctrine dans un controller


```php
namespace BlogBundle\Controller;

use BlogBundle\Entity\Article;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Request;

/**
 * Article controller.
 *
 * Préfix pour toutes les actions de ce controller http://monsite.dev/article/
 * @Route("article")
 */
class ArticleController extends Controller
{
    /**
     * Lister tous les articles.
     *
     * @Route("/", name="article_index") http://monsite.dev/article
     * @Method("GET")
     */
    public function indexAction()
    {
        //récupération de l'entity manager (doctrine)
        $em = $this->getDoctrine()->getManager();

        //récupération de tous les articles
        $articles = $em->getRepository('BlogBundle:Article')->findAll();

        return $this->render('article/index.html.twig', array(
            'articles' => $articles,
        ));
    }
    
    /**
     * Afficher un article
     *
     * @Route("/{id}", name="article_show")  http://monsite.dev/article/1
     * @Method("GET")
     */
    public function showAction(Article $article)
    {
    
        return $this->render('article/show.html.twig', array(
            'article' => $article,
        ));
    }
    
    /**
     * Créer un nouvel article
     *
     * @Route("/new", name="article_new") http://monsite.dev/article/new
     */
    public function newAction(Request $request)
    {
        //nouvel object Article vide
        $article = new Article();
        
        $form = $this->createFormBuilder($article)
                    ->add('title')
                    ->add('content')
                    ->add('save', SubmitType::class, array('label' => 'Create Article'))
                    ->getForm();
        
        
        //si on vient de soumettre le formulaire, notre article vide se remplit avec les données du form
        $form->handleRequest($request);

        //Dans le cas d'une soumission du formulaire
        if ($form->isSubmitted() && $form->isValid()) {
            //Entity manager
            $em = $this->getDoctrine()->getManager();
            
            //On indique à doctrine qu'il y a un nouvel élément
            $em->persist($article);
            //Mise à jour de la BDD
            $em->flush($article);


            //redirection après ajout en base vers le nouvel article
            //redirectToRoute 
            // le premier paramètre est le nom de la route
            // le 2, les paramètres à transmettre, ici l'ID de l'article
            return $this->redirectToRoute('article_show', array('id' => $article->getId()));
        }

        return $this->render('article/new.html.twig', array(
            'article' => $article,
            'form' => $form->createView(),
        ));
    }
    
    /**
     * Afficher un formulaire pour modifier un article
     *
     * @Route("/{id}/edit", name="article_edit") http://monsite.dev/article/1/edit
     * @Method({"GET", "POST"})
     */
    public function editAction(Request $request, Article $article)
    {
    
        $editForm = $this->createFormBuilder($article)
                    ->add('title')
                    ->add('content')
                    ->add('save', SubmitType::class, array('label' => 'Update Article'))
                    ->getForm();
     
        $editForm->handleRequest($request);
    
        if ($editForm->isSubmitted() && $editForm->isValid()) {
            //mise à jour de la BDD
            $this->getDoctrine()->getManager()->flush();
    
            return $this->redirectToRoute('article_show', array('id' => $article->getId()));
        }
    
        return $this->render('article/edit.html.twig', array(
            'article' => $article,
            'edit_form' => $editForm->createView()
        ));
    }
    
}
```

## Pour aller plus loin

Votre principale bible reste est restera [la documentation de Symfony](http://symfony.com/doc/current/index.html)



