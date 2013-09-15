---
title: Les routes GET
status: live
---

Utilisez la méthode `get()` de l'application Slim pour mapper une fonction de rappel à une URI qui est appelée avec une méthode HTTP GET.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:id', function ($id) {
        //Afficher le livre identifié par $id
    });

Dans cet exemple, une requête HTTP GET pour “/books/1” va appeler la fonction de rappel associée, le tout en passant “1” comme argument à cette fonction de rappel.

Le premier argument de la méthode `get()` de l'application Slim est l'URI. Le dernier argument est un objet quelconque qui doit répondre au critère suivant: retourner `true` pour la fonction `is_callable()`.
Typiquement, le dernier argument sera une [fonction anonyme][anon-func]

[anon-func]: http://php.net/manual/fr/functions.anonymous.php
