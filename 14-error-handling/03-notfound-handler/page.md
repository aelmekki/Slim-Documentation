---
title: Gestionnaire d'erreurs de type "Non trouvé"
status: live
---

C'est inéluctable, quelqu'un finira par appeler une page qui n'existe pas. Slim vous permet de définir facilement un gestionnaire de "Non trouvé" avec la méthode `notFound()`. Le gestionnaire de non trouvé sera appelé si aucune route n'est trouvée pour la requête HTTP courante. Cette méthode agit comme un getter et un setter.

### Définir un gestionnaire de non trouvé

Si vous appelez la méthode `notFound()` de Slim avec une fonction comme argument, la méthode enregistrera cette fonction comme le gestionnaire de non trouvé. Sinon, le gestionnaire de base sera appelé.

    <?php
    $app = new \Slim\Slim();
    $app->notFound(function () use ($app) {
        $app->render('404.html');
    });

### Appeler ce gestionnaire

Si vous appelez la méthode `notFound()` de Slim sans argument, elle invoquera  le gestionnaire précédement enregistré.

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) use ($app) {
        if ( $name === 'Charlie' ) {
            $app->notFound();
        } else {
            echo "Hello, $name";
        }
    });
