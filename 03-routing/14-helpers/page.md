---
title: Route Helpers
status: live
---

Slim fourni une panoplie de méthodes d'aide (utilisables via une instance d'application de Slim) qui vous aident à contrôler le flux de votre application.

Notez que les méthodes d'aide `halt()`, `pass()`, `redirect()` et `stop()` utilisent des Exceptions.
Elles lanceront une exception du type `\Slim\Exception\Stop` ou encore `\Slim\Exception\Pass`.
Lancer une Exception dans ces cas est une façon simple de stopper l'exécution du code de l'utilisateur, permettre au framework de prendre le dessus, et immédiatement envoyer la réponse nécessaire au client. Ce comportement peut être surprenant s'il n'est pas attendu. Regardez le code suivant:

    <?php
    $app->get('/', function() use ($app, $obj) {
        try {
            $obj->thisMightThrowException();
            $app->redirect('/success');
        } catch(\Exception $e) {
            $app->flash('error', $e->getMessage());
            $app->redirect('/error');
        }
    });

Si `$obj->thisMightThrowException()` lance une Exception le code tournera comme attendu. Par contre, si aucune exception n'est lancée, l'appel à `$app->redirect()` lancera une Exception du type `\Slim\Exception\Stop` qui sera attrapée par le bloc `catch` de l'utilisateur, qui redirigera le navigateur vers la page d'erreur "/error".
Là où c'est possible, vous devez utiliser des Exceptions typées, comme cela les blocs `catch` sont plus précis pour la gestion de l'erreur.
Dans certaines situations, `thisMightThrowException()` peut être un composent externe que vous appelez et dont vous ne contrôlez rien. Dans ce cas, récupérer chaque type d'Exception n'est parfois pas faisable. 
Pour ces cas, nous pouvons ajuster le code en déplaçant l' `$app->redirect()` après le try/catch pour résoudre ce cas. Comme le traitement s'arrête sur l'erreur de redirection, ce code va s'exécuter comme prévu.

    <?php
    $app->get('/', function() use ($app, $obj) {
        try {
            $obj->thisMightThrowException();
        } catch(Exception $e) {
            $app->flash('error', $e->getMessage());
            $app->redirect('/error');
        }
        $app->redirect('/success');
    });

### Arrêter

La méthode `halt()` de Slim va automatiquement retourner une réponse HTTP avec un code et un corps voulu.
Cette méthode accepte donc deux arguments: le statut HTTP et un message optionnel. Slim va immédiatement stopper l'application et renvoyer une réponse HTTP au client avec les arguments spécifiés (dont le message dans le corps).
Cela va surcharger l'objet `\Slim\Http\Response` existant.

    <?php
    $app = new \Slim\Slim();

    // Renvoyer une erreur 500
    $app->halt(500);

    // Ou si l'utilisateur rencontre une erreur d'accès 
    $app->halt(403, 'Vous ne passerez pas!');

Si vous voulez utiliser un template avec une liste de messages d'erreur, vous devez utiliser la méthode `render()` de l'application Slim.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $errorData = array('error' => 'Permission refusée');
        $app->render('errorTemplate.php', $errorData, 403);
    });
    $app->run();

La méthode `halt()` peut renvoyer tout type de réponse HTTP au client: informel, de succès, redirection, page non trouvée, erreur côté client, ou encore erreur côté serveur.

### Passer

Une route peut dire à l'application Slim de continuer jusqu'à la prochaine route qui fonctionnera avec la méthode `pass()` de l'application.
Quand cette méthode est appelée, Slim va immédiatement stopper l'exécution de la route courante et appeler la prochaine route qui correspond. Si aucune route ne correspond plus, une réponse de type **404 Non Trouvée** est renvoyée au client. Voici un exemple, en considèrent une requête pour “GET /hello/Frank”.

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/Frank', function () use ($app) {
        echo "Vous ne verrez pas cela...";
        $app->pass();
    });
    $app->get('/hello/:name', function ($name) use ($app) {
        echo "Mais vous verrez cela!";
    });
    $app->run();

### Rediriger

C'est simple de rediriger le client à une autre UTL avec la méthode `redirect()` de l'application Slim. Cette méthode accepte 2 arguments: le premier argument est l'URL sur laquelle le client sera redirigé; le second, optionnel, est un statut HTTP. Par défaut, la méthode `redirect()` va renvoyer une réponse de type **302 Redirection Temporaire**

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $app->redirect('/bar');
    });
    $app->run();

Ou si vous voulez utiliser une redirection permanente, vous devez spécifier l'URL de destination en premier argument et le statut HTTP en second argument.

    <?php
    $app = new \Slim\Slim();
    $app->get('/old', function () use ($app) {
        $app->redirect('/new', 301);
    });
    $app->run();

Cette méthode va automatiquement ajouter le "Location: header". La réponse (une redirection) HTTP sera envoyée au client immédiatement.

### Stopper

La méthode `stop()` de l'application Slim va stopper l'application et envoyer la réponse HTTP actuelle au client telle qu'elle est. Rien de plus.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        echo "Vous verrez cela...";
        $app->stop();
        echo "Mais pas cela";
    });
    $app->run();

### URL For

La méthode `urlFor()` vous permet de dynamiquement créer des URLs pour une route nommée. Ainsi, quand un patron de route change, les URLs vont automatiquement se mettre à jour sans briser l'application. Cet exemple montre comment générer des URLs pour une route nommée.

    <?php
    $app = new \Slim\Slim();

    //Créer une route nommée
    $app->get('/hello/:name', function ($name) use ($app) {
        echo "Hello $name";
    })->name('hello');

    //Générer une url pour une route nommée
    $url = $app->urlFor('hello', array('name' => 'Josh'));

Dans cet exemple, `$url` vaut “/hello/Josh”. Pour utiliser la méthode `urlFor()`, vous devez, premièrement, donner un nom à une route. Ensuite, appeler la méthode `urlFor()`. Le premier argument est le nom de la route, et, le deuxième argument est un tableau associatif, utilisé pour remplacer les paramètres d'URL de la route avec les valeurs actuelles; les clés du tableau doivent correspondre avec les paramètres de la route dans l'URI et les valeurs seront utilisées en substitution.
