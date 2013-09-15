---
title: Modes de l'application
status: live
---

C'est une pratique commune que de faire tourner une application web dans un mode dépendant de l'état courant du projet.
Si vous développez l'application, elle tournera en mode de “développement”; si vous la testez, le mode sera “test”; si les développements et tests sont ok, l'application est lancée et tourne en mode “production”.

Slim supporte le concepte des modes que vous pouvez définir vous-même. Par exemple, vous pouvez activer le débogague dans le mode “développement” mais pas dans le mode “production”. L'exemple suivant montre comment configurer Slim différent pour un mode donné.

### Qu'est-ce qu'un mode?

Techniquement, un mode d'application n'est qu'une chaine de caractère - comme “production” ou “développement” - qui dispose d'une fonction de rappel utilisée pour préparer Slim correctement. 
Le mode de l'application peut être n'importe quoi, ce que vous voulez, “test”, “production”, “développement”, ou encore “foo” et même “bar”!

### Comment mettre en place un mode?

<div class="alert alert-info">
    <strong>Attention!</strong> Le mode de l'application peut être défini seulement à l'instanciation et ne peut plus être changé après.
</div>

#### Utiliser une variable d'environnement

Si Slim voit une variable d'environnement nommée "SLIM_MODE", il va définir le mode de l'application comme la valeur de cette même variable.

    <?php
    $_ENV['SLIM_MODE'] = 'production';

#### Utiliser un paramètre d'application

Si aucune variable d'environnement n'est trouvée, Slim va ensuite regarder dans le paramètre de l'application.

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'production'
    ));

#### Mode par défaut

Si aucune des deux valeur n'est trouvée, Slim va définir le mode à “development”.

### Configurer pour un mode spécifique

Après avoir instancié votre application Slim, vous pouvez la configurer pour un mode spécifique avec la méthode `configureMode()` de Slim. Cette méthode accepte 2 arguments: le nom du mode ciblé et une fonction de rappel qui sera appelée imédiatement si le premier argument correspond au mode de l'application.

En considérant que le mode de l'application est “production”. Seul la fonction de rappel associée au mode “production” sera appelée. La fonction de rappel associée au mode “development” sera ignorée tant que le mode n'est pas changé à “development”.

    <?php
    // Définir le mode
    $app = new \Slim\Slim(array(
        'mode' => 'production'
    ));

    // Seulement appelée si le mode est "production"
    $app->configureMode('production', function () use ($app) {
        $app->config(array(
            'log.enable' => true,
            'debug' => false
        ));
    });

    // Seulement appelée si le mode est "development"
    $app->configureMode('development', function () use ($app) {
        $app->config(array(
            'log.enable' => false,
            'debug' => true
        ));
    });
