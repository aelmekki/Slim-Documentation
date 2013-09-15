---
title: Hello World
status: live
---

Instanciez une application Slim:

    $app = new \Slim\Slim();

Définissez une route HTTP GET:

    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name";
    });

Exécutez l'application Slim:

    $app->run();
