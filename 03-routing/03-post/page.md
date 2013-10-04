---
title: Les routes POST
status: live
---

Utilisez la méthode `post()` de l'application Slim pour mapper une fonction de rappel à une URI qui est appelée avec une méthode HTTP POST.

    <?php
    $app = new \Slim\Slim();
    $app->post('/books', function () {
        //Créer un livre
    });

Dans cet exemple, une requête HTTP POST sur “/books” appelera la fonction de rappel associée.

Le premier argument de la méthode `post()` de l'application Slim est l'URI. Le dernier argument est un objet quelconque, qui doit répondre au critère suivant: retourner `true` pour la fonction `is_callable()`.
Typiquement, le dernier argument sera une [fonction anonyme][anon-func]

[anon-func]: http://php.net/manual/fr/functions.anonymous.php
