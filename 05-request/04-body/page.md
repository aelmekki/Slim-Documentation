---
title: Corps de requête
status: live
---

Utilisez la méthode `getBody()` de l'objet `request` pour récupérer le corps HTML envoyé par le client HTTP. C'est très utile pour une application qui lit des requêtes en JSON ou XML.

    <?php
    $app = new \Slim\Slim();
    $body = $app->request->getBody();
