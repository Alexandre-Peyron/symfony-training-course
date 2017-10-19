# Evènements Symfony

Dans cet exercice, nous allons créer une service symfony qui va centraliser l'envoi
des emails de notre application. 


### Mise en place du contexte

> Vous pouvez travailler dans AppBundle

Créez une nouvelle route/controller/view qui affiche un formulaire de contact.

- Nom Prénom
- Email
- Objet
- Message

Ce formulaire peut être créé depuis une entité `Contact` ou directement via le form builder Symfony. Au choix.


### Events

On va maintenant créer un nouvel évènement Symfony.

```php
<?php

namespace AppBundle\Event;

use Symfony\Component\EventDispatcher\Event;

class MailEvent extends Event
{
    const SEND_MAIL = 'event.send.mail.connector';

    /**
     * @var string
     */
    protected $from = null;

    /**
     * @var string
     */
    protected $to = null;

    /**
     * @var string
     */
    protected $object = null;

    /**
     * @var string
     */
    protected $content = null;


    public function __construct($from, $to, $object, $content)
    {
        $this->from = $from;
        $this->to = $to;
        $this->object = $object;
        $this->content = $content;
    }

    /**
     * @return string
     */
    public function getFrom()
    {
        return $this->from;
    }

    /**
     * @param string $from
     */
    public function setFrom($from)
    {
        $this->from = $from;
    }
    
    ...
}
```

Maintenant que notre MailEvent existe, on va dispatcher l'évènement dans le controller lorsque le formulaire de contact est soumis.

Pour cela, faites un `$event = new MailEvent($from, $to, $object, $content)` 

Récupérez l'Event Dispatcher de Symfony et disptachez le.

```php
        $this->get('event_dispatcher')->dispatch(
            MailEvent::SEND_MAIL, $event
        );
```

Très bien ! Maintenant, lorsque le formulaire de contact est soumis, un évènement est dispatché
pour demandé l'envoi d'un mail avec toutes les informations nécessaires.

Malheureusement personne n'est là pour l'écouter :(


### Listener

Votre travail à présent est de créer une service qui va écouter cet évènement pour ensuite envoyer le mail

Voici le début de la class

```php
<?php

namespace AppBundle\EventListener;

use AppBundle\Event\MailEvent;
use Symfony\Component\EventDispatcher\EventSubscriberInterface;

class EventToMailConnector implements EventSubscriberInterface
{
    ...
}

```

A vous de jouer maintenant.

Il faut:
    - déclarer le service
    - déclarer l'écoute sur l'évènement MailEvent::SEND_MAIL
    - coder la fonction d'envoi de mail


> Symfony possède par défaut un bundle pour l'envoi de mail, nommé SwiftMailer
