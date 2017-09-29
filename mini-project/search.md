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
