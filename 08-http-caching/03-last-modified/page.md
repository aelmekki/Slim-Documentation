---
title: Dernière modification
status: live
---

Une application Slim fournit un support intégré pour la mise en cache HTTP en utilisant date de dernière modification de la ressource. Lorsque vous spécifiez une date de dernière modification, Slim indique au client HTTP la date et l'heure à laquelle la ressource actuelle a été modifiée. Le client HTTP envoie alors un en-tête ** If-Modified-Since ** avec chaque requête HTTP suivante pour la donnée (URI) de la ressource. Si la date de dernière modification que vous spécifiez correspond aux en-têtes ** If-Modified-Since ** de requête HTTP,
l'application Slim va retourner une ** 304 ** non modifiée dans la réponse HTTP, ce qui incitera le client HTTP à utiliser son cache et ce qui empêche aussi l'application Slim de servir l'ensemble de la page ou de la ressource ce qui fait économiser bande passante et temps de réponse.

Définir une date de dernière modification avec Slim est très simple. Vous avez seulement besoin d'invoquer la méthode `lastModified()` de Slim () dans votre fonction de rappel, le tout en passant un timestamp UNIX, date de dernière modification de la ressource donnée.
Assurez-vous que le timestamp  de la méthode `lastModified ()` se mette à jour avec la ressource, sinon,
le client HTTP va continuer à se servir son cache...

    <?php
    $app->get('/foo', function () use ($app) {
        $app->lastModified(1286139652);
        echo "Sera mis en cache après cette requête!";
    });
