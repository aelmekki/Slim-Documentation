---
title: Débogage
status: live
---

Vous pouvez activer le débogage à l'instanciation de Slim:

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

Vous pouvez le faire aussi pendant l'exécution avec la méthode `config()` de Slim:

    <?php
    $app = new \Slim\Slim();

    // Activer le débogage (activé par défaut)
    $app->config('debug', true);

    // Désactiver le débogage
    $app->config('debug', false);

Si le débogage est activé et qu'une exception ou une erreur se produit, un écran de diagnostic apparaîtra avec la description de l'erreur, le fichier affecté, la ligne dans le fichier et une stack trace. Si le débogage est désactivé, le gestionnaire d'erreur personnalisé sera appelé à la place.
