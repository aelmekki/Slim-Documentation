---
title: En-têtes de réponse
status: live
---


La réponse HTTP retournée au client HTTP aura un en-tête. Un en-tête HTTP est une liste de clés-valeurs qui fournit des métadonnées sur la réponse HTTP. Vous pouvez utiliser l'objet response de l'application Slim pour assigner cet en-tête. L'objet response dispose d'une propriété publique `headers` qui est une instance de `\Slim\Helper\Set`; cela fournit une interface simple, standardisée, pour manipuler les en-têtes de réponse HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->response->headers->set('Content-Type', 'application/json');

Vous pouvez aussi récuperer les en-têtes de l'objet response aussi:

    <?php
    $contentType = $app->response->headers->get('Content-Type');

Si un en-tête avec un nom donné n'existe pas, `null` est renvoyé. Vous pouvez spécifier des noms d'en-têtes en majuscules, minuscules, mixés, avec des underscores ou des tirets. Utilisez la convention de nommage avec laquelle vous vous sentez à l'aise.
