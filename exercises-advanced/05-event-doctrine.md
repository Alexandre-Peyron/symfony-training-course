# Evènements Doctrine

Dans cet exercice, nous allons nous servire des évènements Doctrine pour 
modifier automatiquement nos entités.

[La documentation associée](https://symfony.com/doc/current/doctrine/event_listeners_subscribers.html)
mais il n'est pas nécessaire de l'ouvrir tout de suite.

### Mise en place du contexte

> Vous pouvez travailler sur un nouveau projet, dans AppBundle 

Créez une nouvelle entité Invoice (en français facture) qui possède les propriétés suivantes :

- clientName - string
- clientAcronym - string
- reference - string
- invoiceDate - date - (date de référence sur la facture)
- dueDate - date - (date limite de paiement )
- object - string - (objet de la facture)
- createdAt - datetime - (date de création)
- updatedAt - datetime - (date de dernière mise à jour de la facture)

Vous pouvez utiliser le CRUD pour générer les actions de bases sur Invoice.


### Le Formulaire

Le formulaire a généré contient des champs dont nous n'avons pas besoin. 
Ils seront renseignés automatiquement à l'update ou au persist de l'entité.

Pour commencer, supprimez donc les champs suivant :
- createdAt
- updatedAt

### Service listener

Nous allons maintenant créer et déclarer un service 
qui va être appelé à chaque persist et update de l'entité.

Créez le fichier suivant : AppBundle/EventListener/InvoiceListener

```php
<?php

namespace AppBundle\EventListener;

use AppBundle\Entity\Invoice;
use Doctrine\ORM\EntityManager;
use Doctrine\ORM\Event\LifecycleEventArgs;
use Doctrine\ORM\Event\PreUpdateEventArgs;

class InvoiceListener
{
    /**
     * On pre persist entity invoice
     *
     * @param LifecycleEventArgs $args
     */
    public function prePersist(LifecycleEventArgs $args)
    {
        /** @var $entity Invoice */
        $entity = $args->getEntity();

        $this->setCreatedAt($entity);
    }

    /**
     * On pre update entity invoice
     *
     * @param PreUpdateEventArgs $args
     */
    public function preUpdate(PreUpdateEventArgs $args)
    {
        /** @var $entity Invoice */
        $entity = $args->getEntity();

        $this->setUpdatedAt($entity);
    }

    /**
     * Set Created At datetime
     *
     * @param $entity Invoice
     */
    private function setCreatedAt($invoice)
    {
        if (!$invoice instanceof Invoice) {
            return;
        }

        $invoice->setCreatedAt(new \DateTime('now'));
    }

    /**
     * Set Updated At datetime
     *
     * @param $entity Invoice
     */
    private function setUpdatedAt($invoice)
    {
        if (!$invoice instanceof Invoice) {
            return;
        }

        $invoice->setUpdatedAt(new \DateTime('now'));
    }
}
```

Maintenant on déclare le listener dans AppBundle/Resources/Config/Services.yml

```yaml
services:
    invoice.event_listener:
        class: AppBundle\EventListener\InvoiceListener
        tags:
            - { name: doctrine.event_listener, event: prePersist }
            - { name: doctrine.event_listener, event: preUpdate }
```

Retestez votre formulaire Invoice, maintenant createdAt et updatedAt sont automatiquement renseignés.


### DueDate

A votre tour maintenant. Améliorez la class InvoiceListener pour renseigner 
automatiquement la DueDate. 

Elle correspond à la InvoiceDate + 30 jours


### Reference

Même travail pour la référence de la facture.
Format:  Acronyme Client | Année | Mois | Jour | ID unique si la référence existe déjà
