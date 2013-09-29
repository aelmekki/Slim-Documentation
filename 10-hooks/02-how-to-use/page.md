---
title: Comment utiliser les crochets?
status: live
---

Une fonction est assignée à un crochet en utilisant la méthode `hook()` de l'application Slim:

    <?php
    $app = new \Slim\Slim();
    $app->hook('le.nom.du.crochet', function () {
        //Faire quelquechose
    });

Le premier argulent est le nom du crochet, le second est la fonction. Chaque crochet maintient une liste de priorités des fonctions qui lui sont liées. Par défaut, chaque fonction liée à un crochet a une priorité de 10. Vous pouvez changer la priorité en définissant un troisième paramètre, entier, à la fonction `hook()`:

    <?php
    $app = new \Slim\Slim();
    $app->hook('le.nom.du.crochet', function () {
        //Faire quelquechose
    }, 5);

L'exemple ci-dessus assigne une priorité de 5 à la fonction. Quand le crochet est appelé, il va trier les fonctions qui lui sont liées par priorité (ascendentes). Une fonction avec une priorité de 1 sera appelée avant une fonction de priorité 10.

Un crochet ne passe pas d'argument à ses fonctions. Si une fonction a besoin d'accéder à l'application Slim, vous pouvez l'injecter dans la fonction de rappel avec le mot-clé `use` ou avec la méthode statique `getInstance()`:

    <?php
    $app = new \Slim\Slim();
    $app->hook('le.nom.du.crochet', function () use ($app) {
        // Faire quelquechose
    });
