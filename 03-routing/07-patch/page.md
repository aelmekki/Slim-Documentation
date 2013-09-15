---
title: Les routes PATCH
status: live
---

Utilisez la méthode `patch()` de l'application Slim pour mapper une fonction de rappel à une URI qui est appelée avec une méthode HTTP PATCH.

    <?php
    $app = new \Slim\Slim();
    $app->patch('/books/:id', function ($id) {
        // Patcher le livre avec l'ID donné
    });

Dans cet exemple, une requête HTTP PATCH pour “/books/1” va appeler la fonction de rappel associée, le tout en passant “1” comme argument à cette fonction de rappel.

Le premier argument de la méthode `patch()` de l'application Slim est l'URI. Le dernier argument est un objet quelconque qui doit répondre au critère suivant: retourner `true` pour la fonction `is_callable()`.
Typiquement, le dernier argument sera une [fonction anonyme][anon-func]

[anon-func]: http://php.net/manual/fr/functions.anonymous.php
