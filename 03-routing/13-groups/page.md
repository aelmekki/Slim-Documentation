---
title: Groupe de routes
status: live
---

Slim vous permet de regrouper des routes liées. C'est utile lorsque vous utilisez la même URL (ou segments d'URL) pour plusieurs routes. La meilleure explication est un exemple. Disons que vous créez une API pour des livres.

    <?php
    $app = new \Slim\Slim();

    // API group
    $app->group('/api', function () use ($app) {

        // Groupe "Bibliothèque"
        $app->group('/library', function () use ($app) {

            // Récupérer un livre avec son id
            $app->get('/books/:id', function ($id) {

            });

            // Mettre à jour un livre avec son id
            $app->put('/books/:id', function ($id) {

            });

            // Supprimer un livre avec son id
            $app->delete('/books/:id', function ($id) {

            });

        });

    });

Les routes définies ci-dessus seront accessibles par, respectivement:

    GET    /api/library/books/:id
    PUT    /api/library/books/:id
    DELETE /api/library/books/:id

Les groupes de routes sont très utiles pour regrouper des routes "liées" sans avoir à répéter le segment d'URL au complet pour chaque définition de route.
