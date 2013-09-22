---
title: Expiration
status: live
---

Utilisé en conjonction avec les méthodes `etag()` ou `lastModified()`, la méthode `expires()` met un en-tête HTTP de type **Expires** dans la réponse pour informer  le client HTTP quand son cache pour la ressource actuelle doit être considéré comme expiré. Le client HTTP continuerade se servir de son cache côté client tant que la date d'expiration n'est pas atteinte.

La méthode `expires()` accepte un seul argument: un timestamp UNIX (entier), ou une chaîne de caractères qui sera parsée par `strtotime()`.

    <?php
    $app->get('/foo', function () use ($app) {
        $app->etag('ressource-id-unique');
        $app->expires('+1 week');
        echo "Cela sera stocké dans le cache client pendant 1 semaine";
    });
