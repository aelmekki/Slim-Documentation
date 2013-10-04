---
title: Les routes OPTIONS
status: live
---

Utilisez la méthode `options()` de l'application Slim pour mapper une fonction de rappel à une URI qui est appelée avec une méthode HTTP OPTIONS.

    <?php
    $app = new \Slim\Slim();
    $app->options('/books/:id', function ($id) {
        //Retourner les en-têtes
    });

Dans cet exemple, une requête HTTP OPTIONS pour “/books/1” va appeler la fonction de rappel associée, le tout en passant “1” comme argument à cette fonction de rappel.

Le premier argument de la méthode `options()` de l'application Slim est l'URI. Le dernier argument est un objet quelconque qui doit répondre au critère suivant: retourner `true` pour la fonction `is_callable()`.
Typiquement, le dernier argument sera une [fonction anonyme][anon-func]

### Surcharge de méthode

Malheureusement, les navigateurs web récents ne fournissent pas de support natif pour les requêtes HTTP DELETE. Pour supprimer cette limitation, assurez-vous que l'attribut *method* de votre formulaire HTML est “post”, ensuite, ajoutez une surcharge de méthode dans le formulaire HTML comme cela:

    <form action="/books/1" method="post">
        ... éléments du formulaire ici ...
        <input type="hidden" name="_METHOD" value="OPTIONS"/>
        <input type="submit" value="Récupérer les options pour le livre"/>
    </form>

Si vous utilisez [Backbone.js][backbone] ou un client HTTP en lignes de commandes, vous pouvez également surcharger la méthode HTTP en utilisant l'en-tête **X-HTTP-Method-Override**

[anon-func]: http://php.net/manual/fr/functions.anonymous.php
[backbone]: http://documentcloud.github.com/backbone/
