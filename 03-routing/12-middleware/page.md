---
title: Middleware de routage
status: lives
---

Slim vous permet d'associer des middleware à certaines routes. Quand une route donnée correspond à la requête HTTP et est appelée, Slim va d'abbord appeler les middlewares associés, dans l'ordre dans lesquels ils sont définis.

### Qu'est-ce qu'un middleware de routage?

Un middleware de routage est n'importe quoi qui retour `true` à `is_callable`. Un middleware de routage sera appelé dans l'ordre dans lequel il a été défini avant que la fonction de rappel soit appelée. 

### Comment j'ajoute un middleware de routage?

Lorsque vous définissez une nouvelle route d'application avec les méthodes `get()`, `post()`, `put()`ou `delete()`, vous devez définir un patron de routage et une fonction qui sera appelée quand la route correspond à une requête HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        //Faire quelque chose
    });

Dans l'exemple ci-dessus, le premier argument est le patron de routage. Le dernier argument est une fonction de rappel qui sera appelée quand une requête HTTP correspond à la route. Le patron de route doit toujours être le premier argument. La fonction de rappel doit toujours être le dernier argument

Vous pouvez associer des middlewares à cette route en passant chaque middleware comme un argument au (vous vous en doutez) milieu... Comme cela:

    <?php
    function mw1() {
        echo "Je suis un middleware!";
    }
    function mw2() {
        echo "Je suis un middleware aussi!";
    }
    $app = new \Slim\Slim();
    $app->get('/foo', 'mw1', 'mw2', function () {
        //Faire quelque chose
    });

Quand la route /foo est appelée, les fonctions `mw1` et `mw2` seront appelées dans l'ordre avant que la fonction de rappel soit appelée.

Admettons que vous voulez authentifier l'utilisateur courant et savoir son rôle pour une route spécifique. Vous pouvez utiliser cela:

    <?php
    $authenticateForRole = function ( $role = 'member' ) {
        return function () use ( $role ) {
            $user = User::fetchFromDatabaseSomehow();
            if ( $user->belongsToRole($role) === false ) {
                $app = \Slim\Slim::getInstance();
                $app->flash('error', 'Login required');
                $app->redirect('/login');
            }
        };
    };
    $app = new \Slim\Slim();
    $app->get('/foo', $authenticateForRole('admin'), function () {
        //Afficher le panneau d'administration
    });

### Quels arguments sont passés dans chaque middleware de routage?

Chaque middleware est appelé avec 1 argument, l'objet `\Slim\Route` qui correspond à ce moment.

    <?php
    $aBitOfInfo = function (\Slim\Route $route) {
        echo "La route courante est " . $route->getName();
    };

    $app->get('/foo', $aBitOfInfo, function () {
        echo "foo";
    });
