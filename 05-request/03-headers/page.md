---
title: En-têtes de requête
status: live
---

Une application Slim va automatiquement parser touts les en-têtes d'une requête HTTP. Vous pouvez accéder à ces en-têtes en utilisant le membre public `headers` de l'objet `request`. La propriété `headers` est une instance de `\Slim\Helper\Set`, cela veut dire qu'il fournit une interface simple et standard pour interagir avec les en-têtes de la requête HTTP.

    <?php
    $app = new \Slim\Slim();

    // Récuperer les en-têtes dans un tableau associatif
    $headers = $app->request->headers;

    // Récuperer l'en-tête ACCEPT_CHARSET
    $charset = $app->request->headers->get('ACCEPT_CHARSET');

Les spécifications HTTP précisent que les noms d'en-tête peuvent être en majuscule, minuscules ou un mixte des deux. Slim est suffisamment intelligent pour parser et retourner une valeur d'en-tête quelle qu'en soit l'écriture que vous avez utilisé (minuscules, majuscules, mixte) pour le nom, le tout avec soit des underscores ou des tirets. Utilisez donc les conventions de nommage que vous préférez.
