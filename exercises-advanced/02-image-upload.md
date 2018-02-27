# Upload d'image dans Symfony

Dans cet exercice, nous allons créer un formulaire pour 
uploader une ou des images sur notre serveur.

### Entity

Dans un premier temps, nous allons modifier notre entité. 
Partons sur l'exemple d'un article auquel nous ajoutons une cover.

> D'une part nous allons avoir une propriété cover, une chaine de caractère enregistrée en BDD, 
qui correspond au nom de l'image avec son extension. Ex: 32498732938.jpg

> D'autre part, une propriété file, non enregistrée en base qui correspondra à notre objet uploadé.


```php
<?php
namespace Admin\BlogBundle\Entity;

use Doctrine\ORM\Mapping as ORM;
use Symfony\Component\HttpFoundation\File\File;
use Symfony\Component\Validator\Constraints as Assert;

/**
 * Article
 *
 * @ORM\Table(name="article")
 * @ORM\Entity(repositoryClass="Admin\BlogBundle\Repository\ArticleRepository")
 */
class Article
{
    /**
    * @const path to cover directory
    */
    const COVER_DIRECTORY = '/uploads/cover/';

    // ...

    /**
     * @var string
     *
     * @ORM\Column(type="string")
     */
    private $cover;

    /**
     * @var File
     *
     * @Assert\NotBlank(message="S'il vous plait, ajoutez une image de couverture")
     * @Assert\File(mimeTypes={ "image/jpeg","image/png"  })
     */
    private $file;

    // ...

    /**
     * Get Cover
     *
     * @return string
     */
    public function getCover()
    {
        return $this->cover;
    }

    /**
     * Set cover
     *
     * @param string $cover
     *
     * @return Article
     */
    public function setCover($cover)
    {
        $this->cover = $cover;

        return $this;
    }

    /**
     * @return File
     */
    public function getFile()
    {
        return $this->file;
    }

    /**
     * @param File $file
     */
    public function setFile($file)
    {
        $this->file = $file;
    }
    
    /**
     * On part de notre class et on remonte jusqu'au dossier web
     * Chemin physique sur le serveur du dossier d'upload
     *
     * @return string
     */
    public function getCoverUploadDirectory()
    {
        return __DIR__ . "/../../../../web" . self::COVER_DIRECTORY;
    }

    /**
     * Chemin physique de l'image sur le serveur  
     * 
     * @return string
     */
    public function getCoverAbsolutePath()
    {
        return $this->getCoverUploadDirectory() . $this->getCover();
    }

    /**
     * Chemin de l'image via l'URL, servira dans pour l'affichage dans les templates twig
     *
     * @return string
     */
    public function getCoverWebPath()
    {
        return self::COVER_DIRECTORY . $this->getCover();
    }
}

```


### Form

Maintenant, il faut mettre à jour notre formulaire d'article pour gérer l'upload.
On ajoute, dans le formulaire, seulement la propriété file, la cover sera mise à jour dynamiquement par la suite.

```php
<?php

namespace Admin\BlogBundle\Form;

use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\FileType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class ArticleType extends AbstractType
{
    /**
     * {@inheritdoc}
     */
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            // ...
            ->add('file', FileType::class, array('label' => 'Image de cover (JPG ou PNG)'))
            // ...
        ;
    }
    
    /**
     * {@inheritdoc}
     */
    public function configureOptions(OptionsResolver $resolver)
    {
        $resolver->setDefaults(array(
            'data_class' => 'Admin\BlogBundle\Entity\Article'
        ));
    }
}
```

Et de même dans le view pour afficher le champ

```twig
{{ form_start(form) }}
    {# ... #}

    {{ form_row(form.file) }}
{{ form_end(form) }}
```

### Enregistrement du fichier

A présent, notre entité est à jour, notre formulaire aussi, il reste le controller pour déplacer le fichier sur le serveur.


```php
<?php
namespace AppBundle\Controller\ArticleController;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Request;
use AppBundle\Entity\Article;
use AppBundle\Form\ProductType;

class ArticleController extends Controller
{
    /**
     * @Route("/article/new", name="app_article_new")
     */
    public function newAction(Request $request)
    {
        $article = new Article();
        $form = $this->createForm(ArticleType::class, $article);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            // $file contient l'image nouvellement uploadée
            /** @var Symfony\Component\HttpFoundation\File\UploadedFile $file */
            $file = $article->getFile();

            // Génération d'un nom unique pour l'image (pour éviter les collisions à l'enregistrement)
            $fileName = md5(uniqid()).'.'.$file->guessExtension();

            // Déplacement l'image dans le dossier
            $file->move(
                $article->getCoverUploadDirectory(),
                $fileName
            );

            // On met à jour la propriété cover
            $article->setCover($fileName);

            // ... persist $article

            return $this->redirect($this->generateUrl('app_article_list'));
        }

        return $this->render('product/new.html.twig', array(
            'form' => $form->createView(),
        ));
    }
}
```

### Twig

Pour afficher notre image nouvellement uploadée

```twig
<img src="{{ asset(article.getCoverWebPath) }}" />
```
