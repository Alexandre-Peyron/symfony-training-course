# Recherche

Le but de ce mini projet est de créer une page de recherche et filtrage de produits.
Voici un [exemple](https://www.amazon.fr/s/ref=sr_nr_n_1?fst=asa%3Aoff&rh=n%3A6359781031%2Ck%3Apates&keywords=pates&ie=UTF8&qid=1506586095&rnid=1703605031).

### Les entités 

Dans un premier temps, notre projet va être composé de 3 entités :

> Product (ManyToOne Type) (ManyToOne Brand)
> - ref         | string | Référence unique du produit, ex: #20170930PC24
> - name        | string
> - description | text
> - is_enabled  | boolean
> - is_premium  | boolean | Possibilité d'envoi en mode premium
> - price       | float 
> - note        | integer | Note du produit, de 0 à 5 étoiles
> - created_at  | datetime
> - updated_at  | datetime

> Type (OneToMany Product)
> - name | string
> - description | text

> Brand (OneToMany Product)
> - name | string
> - description | text

Nous avons donc un produit qui est associé à un type et une marque.

Le premier travail est donc de générer et configurer toutes les entités puis d'ajouter des données dans la BDD.

### La vue

Ici rien de très compliqué, on va travailler sur une seule vue.

Pour commencer, affichez la liste des produits sans filtre pour le moment.

Préparez une colonne sur la gauche pour le futur formulaire.

### Le formulaire simple

Créez une classe de formulaire qui pour le moment va traiter les informations de bases de notre produit (donc pas la marque, ni le type).

Affichez le formulaire dans la colonne de gauche.

Testez la validité et la soumission du formulaire.

### La requête

Cette fois, on ne met rien à jour dans la BDD. On va se servir des données soumises dans le formulaire pour modifier la requête qui va lister nos produits.

```php
  $request->request->get('form'); //récupère un tableau contenant toutes les valeurs du formulaire
```

```php
  $request->request->get('form')['price']; 
```

Pour la requête, on va ici travailler avec le [query builder de doctrine](https://symfony.com/doc/current/doctrine.html#querying-for-objects-using-doctrine-s-query-builder) directement dans le controller pour le moment.

```php
$price = $request->request->get('price');

$repository = $this->getDoctrine()->getRepository(Product::class);

$query = $repository->createQueryBuilder('p')
    
if($price > 0) {
    $query->where('p.price > :price')
          ->setParameter('price', $price)
}

$query->orderBy('p.price', 'ASC')
      ->getQuery();

$products = $query->getResult();

```



### La pagination

Afficher seulement 10 articles à la fois. Générer une pagination.
