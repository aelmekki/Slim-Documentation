---
title: Généralités sur les injections de dépendances
status: live
---

Slim dispose d'un localisateur de ressources intégré, il permet de facilement injecter des objets dans une application Slim ou de surcharger n'importe lequel des objets internes de Slim (par exemple Request, Response, Log).

## Injecter des valeurs simples

Si vous voulez utiliser Slim comme un simple "magasin" de clé-valeurs, c'est aussi simple que cela:

    <?php
    $app = new \Slim\Slim();
    $app->foo = 'bar';

Maintenant, vous pouvez récupérer cette valeur n'importe où par `$app->foo` et obtenir `bar`.

## En utilisant le localisateur de ressources

Vous pouvez aussi utiliser Slim comme un localisateur de ressources, en injectant des fonctions qui définissent comment vos objets seront construits. Quand la ressource est appelée, la fonction sera invoquée et la ressource retournera la valeur de sortie de la fonction:

    <?php
    $app = new \Slim\Slim();

    // Méthode pour créer un UUID
    $app->uuid = function () {
        return exec('uuidgen');
    };

    // Obtenir un nouvel UUID
    $uuid = $app->uuid;

### Resources en mode Singleton 

Parfois; vous voulez que votre ressource reste la même chaque fois qu'elle est demandée
(i.e. En fait, des singletons dans l'application Slim). Facile:

    <?php
    $app = new \Slim\Slim();

    // Définit une ressource de Log
    $app->container->singleton('log', function () {
        return new \My\Custom\Log();
    });

    // Obtenir la ressource de log
    $log = $app->log;

Chaque fois que vous demandez la ressource de log par `$app->log`, cela retournera la même instance.

### Fonctions comme ressource

Et comment faire si vous voulez littéralement stocker une fonction comme valeur et ne pas l'invoquer? Vous pouvez le faire comme cela:

    <?php
    $app = new \Slim\Slim();

    // Définir la fonction
    $app->myClosure = $app->container->protect(function () {});

    // Retourne la fonction plutôt que l'invoquer
    $myClosure = $app->myClosure;
