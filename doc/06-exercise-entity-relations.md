#Les relations

Première chose à faire, comme toujours, ouvrir la [documentation](http://symfony.com/doc/current/doctrine/associations.html), 
[ici aussi](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/association-mapping.html).
(Les annotations dans la doc doctrine sont valables dans SF si on ajoute @ORM\ devant)

Le but de l'exercice est de comprendre et mettre en place des relations entre les entités.



###OneToOne

Une relation OneToOne signifie qu'un élément d'une table est associé à un unique élement d'une autre table (et inversement).
C'est un cas relativement rare, mais le principal usage se fait dans les relations parent > enfant.
Exemple: un article parent d'un autre. La table faire référence à elle même, ça s'appelle du `self-referencing`

- Créez une relation de self-referencing sur l'une de vos entités
- mettre à jour la base de données

```php
    /**
     * @OneToOne(targetEntity="Article")
     * @JoinColumn(name="article_id", referencedColumnName="id")
     */
    private $article_parent;
```


###ManyToOne

Pour comprendre une relation ManyToOne dans exemple, on va créer une nouvelle entité `ArticleType` avec les champs 'name' et 'description'.

Donc un article possède un seul type, un type peut être associé à plusieurs articles.

Maintenant créez la relation entre les 2 entités.

```php
    class Article
    {
        // ...
    
        /**
         * @ORM\ManyToOne(targetEntity="ArticleType", inversedBy="articles")
         * @ORM\JoinColumn(name="article_type_id", referencedColumnName="id")
         */
        private $articleType;
    }
```

> **targetEntity** correspond au nom de l'entité cible. 
Si jamais elle ne se trouve pas dans le même dossier/bundle, il faut mettre le namespace complet

> **inversedBy** correspond à la variable utilisée dans l'entité cible.

> **name** correspond au nom du champ en base

> **referencedColumnName** correspond à la clé primaire d'article


```php
    use Doctrine\Common\Collections\ArrayCollection;
    
    class ArticleType
    {
        // ...
    
        /**
         * @ORM\OneToMany(targetEntity="Article", mappedBy="articleType")
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
 

###ManyToMany
