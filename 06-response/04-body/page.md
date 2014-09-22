---
title: Corps de la Réponse
status: live
---

La réponse HTTP renvoyée au client HTTP aura un corps. Le corps HTTP est le contenu réel de la réponse HTTP délivrée au client. Vous pouvez utiliser l'objet de réponse de l'application Slim pour définir le corps de la réponse HTTP:

    <?php
    $app = new \Slim\Slim();

    // Overwrite response body
    $app->response->setBody('Foo');

    // Append response body
    $app->response->write('Bar');

Lorsque vous écrasez ou ajoutez le corps de l'objet de réponse, l'objet de réponse définira automatiquement l'en-tête 
**Content-Length** (longueur de contenu) sur la base de la taille en octet du corps de la nouvelle réponse.

Vous pouvez aller chercher le corps de l'objet de réponse comme suit:

    <?php
    $body = $app->response->getBody();

Habituellement, vous n'aurez jamais besoin de régler manuellement le corps de la réponse avec les méthodes `setBody()` ou `write()`;l'application Slim le fera pour vous. Chaque fois que vous répétez `echo()` le contenu à l'intérieur de la fonction de rappel d'un itinéraire, le contenu de la répétition `echo()`est capturé dans une mémoire tampon de sortie et ajouté au corps de réponse avant que la réponse HTTP ne soit renvoyée au client.
