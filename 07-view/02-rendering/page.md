---
title: Génération de rendus
status: live
---

Vous pouvez utiliser la méthode `render()` pour demander à l'objet view actuel de générer le rendu d'un template avec un nombre donné de variables. La méthode `render()` de Slim va `echo()` la sortie retournée par l'objet de vue pour qu'elle soit capturée par un buffer de sortie et ajoutée automatiquement au corps de la réponse (body de l'objet response). Cela ne garantit en rien comment le template sera rendu; c'est délégué à l'objet view.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:id', function ($id) use ($app) {
        $app->render('myTemplate.php', array('id' => $id));
    });

Si vous devez passer des données depuis la fonction de rappel de la route à l'objet view, vous devez explicitement le faire en passant un tableau comme second paramètre de la méthode `render()` comme cela:

    <?php
    $app->render(
        'myTemplate.php',
        array( 'name' => 'Josh' )
    );

Vous pouvez aussi définir le statut de réponse HTTP quand vous générez un rendu de modèle:

    <?php
    $app->render(
        'myTemplate.php',
        array( 'name' => 'Josh' ),
        404
    );
