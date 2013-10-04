---
title: Méthodes HTTP personnalisées
status: live
---

### Une route, plusieurs méthodes HTTP

Parfois, vous allez avoir besoin qu'une route fonctionne avec plusieurs méthodes HTTP, ou encore qu'une route fonctionne avec une méthode HTTP personnalisée. 
Vous pouvez gérer ces deux cas grâce à la méthode `via()` de l'objet Route. Cet exemple montre comment mapper une URI à une fonction de rappel qui va gérer plusieurs méthodes HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "Je réponds à de multiples méthodes HTTP!";
    })->via('GET', 'POST');
    $app->run();

La route définie dans cet exemple va répondre autant pour les requêtes GET que POST sur URI “/foo/bar”.
Spécifiez toutes les méthodes HTTP appropriées comme une liste de chaînes de caractères en argument à la méthode `via()` de l'objet Route. Comme les autres méthodes de Route (par exemple `name()` et `conditions()`), la méthode `via()` est chaînable:

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "La classe, hein?";
    })->via('GET', 'POST')->name('foo');
    $app->run();

### Une route, des méthodes HTTP personnalisées

La méthode `via()` de l'objet Route n'est pas limitée aux seules méthodes GET, POST, PUT, DELETE ou OPTIONS. Vous pouvez très bien spécifier vos propres méthodes HTTP (par exemple si vous répondez aux requêtes HTTP WebDAV). Vous pouvez définir une route qui répond à une requête HTTP personnalisée “FOO” comme cela: 

    <?php
    $app = new \Slim\Slim();
    $app->map('/hello', function() {
        echo "Hello";
    })->via('FOO');
    $app->run();
