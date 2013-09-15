---
title: Noms de route
status: live
---

Slim vous permet d'assigner un nom à une route. Nommer une route vous permet de générer dynamiquement les URLs en utilisant la méthode d'aide `urlFor()`. Lorsque vous utilisez la méthode `urlFor()` pour créer des URLs, vous pouvez changer de patron de route sans casser votre application. Voici un exemple de route nommée:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name!";
    })->name('hello');

Vous pouvez maintenant générer des URLs pour cette route en utilisant la méthode `urlFor()`, décrite plus tard dans cette documentation.
La méthode `name()` est aussi chaînable:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name!";
    })->name('hello')->conditions(array('name' => '\w+'));
