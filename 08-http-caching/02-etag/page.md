---
title: ETag
status: live
---

Une application Slim fournit un support de base pour le cache HTTP avec les ETags. Un en-tête ETag est un identifiant unique pour une ressource URI. Quand un en-tête ETag est assigné avec la méthode `etag()` de Slim, le client HTTP enverra un en-tête **If-None-Match** avec chaque requête HTTP de la même ressource URI. Si la valeur de l'ETag pour la ressource de l'URI correspond au **If-None-Match**, l'application retounera une réponse **304 Not Modified**, ce qui spécifie au client HTTP de continuer à utiliser son cache; cela permet aussi d'éviter à Slim de fournir entièrement la ressource URI, ce qui permet de sauver de la bande passante et de répondre plus rapidement.

Fournir un ETag avec Slim est très simple. Utilisez la méthode `etag()` dans votre fonction de rappel, en passant comme argument un ID unique.


    <?php
    $app->get('/foo', function () use ($app) {
        $app->etag('id-unique');
        echo "Cela sera mis en cache après cette requête!";
    });

Voila. Soyez sûr que l'ID de l'ETag est unique pour une ressource donnée. De plus, vérifiez que votre ETag change quand votre ressource change; sinon, le client HTTP va continuer de se servir de son cache.