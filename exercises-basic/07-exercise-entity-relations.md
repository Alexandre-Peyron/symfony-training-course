# Les relations

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/doctrine/associations.html) 
et [ici aussi](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/association-mapping.html).

> Les annotations dans la documentation doctrine sont valables dans SF si on ajoute @ORM\ devant.

Le but de l'exercice est de comprendre et mettre en place des relations entre les entités.

> Les relations dans Symfony correspondent aux jointures au niveau de MySQL. [ici](https://openclassrooms.com/courses/concevez-votre-site-web-avec-php-et-mysql/les-jointures-entre-tables) un article bien construit sur les jointures.

### ManyToOne

Pour comprendre une relation ManyToOne dans exemple, créons une nouvelle entité `Category` avec les champs 'name' et 'description'.

**Donc un article possède une seule catégorie, une catégorie peut être associée à plusieurs articles.**

Une fois l'entité générée en ligne de commande, créez la relation entre les 2 entités.

```php
    class Article
    {
        // ...
    
        /**
         * @ORM\ManyToOne(targetEntity="Category", inversedBy="articles")
         * @ORM\JoinColumn(name="category_id", referencedColumnName="id")
         */
        private $category;
    }
```

> **targetEntity** correspond au nom de l'entité cible. 
Si jamais elle ne se trouve pas dans le même dossier/bundle, il faut mettre le namespace complet

> **inversedBy** correspond à la variable utilisée dans l'entité cible.

> **name** correspond au nom du champ en base

> **referencedColumnName** correspond à la clé primaire d'article


```php
    use Doctrine\Common\Collections\ArrayCollection;
    
    class Category
    {
        // ...
    
        /**
         * @ORM\OneToMany(targetEntity="Article", mappedBy="category")
         */
        private $articles;
    
        public function __construct()
        {
            $this->articles = new ArrayCollection();
        }
    }
```
> **targetEntity** correspond à l'entité cible

> **mappedBy** correspond à la variable utilisée dans l'entité cible
 
- Mettre à jour les `getter` et `setter` avec `php bin/console make:entity --regenerate` avec en paramètre le namespace de l'entity `App\Entity\MyEntity`
- mettre à jour la base de données `php bin/console doctrine:schema:update --force`

### OneToOne

Une relation OneToOne signifie qu'un élément d'une table est associé à un unique élement d'une autre table (et inversement).
C'est un cas relativement rare, mais le principal usage se fait dans les relations parent > enfant.
Exemple: un article parent d'un autre. La table fait référence à elle même, ça s'appelle du `self-referencing`

- Créez une relation de self-referencing sur l'une de vos entités
- Mettre à jour les `getter` et `setter` avec `php bin/console make:entity --regenerate` (`App\Entity\MyEntity`)
- mettre à jour la base de données `php bin/console doctrine:schema:update --force`

```php
    /**
     * @ORM\OneToOne(targetEntity="Article")
     * @ORM\JoinColumn(name="article_id", referencedColumnName="id")
     */
    private $article_parent;
```

### ManyToMany

La relation ManyToMany est la plus complexe. Dans notre exemple, on peut créer une nouvelle
entité `Tag`. Un article peu avoir plusieurs tags, et un tag plusieurs articles.

Maintenant créez la relation entre les 2 entités.

```php

    class Article
    {
       //...
    
        /**
        * @ORM\ManyToMany(targetEntity="Tag", inversedBy="articles", cascade={"persist"})
        * @ORM\JoinTable(name="article_tags")
        */
        */
        private $tags;
        
        
        public function __construct()
        {
            $this->tags = new ArrayCollection();
        }
        
    }

```

```php

    class Tag
    {
        //...
    
        /**
         * @ORM\ManyToMany(targetEntity="Article", mappedBy="tags")
         */
        private $articles;
    
        public function __construct() {
            $this->articles = new ArrayCollection();
        }
             
    }

```


- Mettre à jour les `getter` et `setter` avec `php bin/console make:entity --regenerate` (`App\Entity\MyEntity`)
- mettre à jour la base de données `php bin/console doctrine:schema:update --dump-sql --force`

> En regardant votre BDD, vous pouvez vous rendre contre que la table intermédiaire a été créé automatiquement
