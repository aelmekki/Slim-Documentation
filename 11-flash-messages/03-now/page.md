---
title: "Flash" Maintenant
status: live
---

La méthode `flashNow()` de l'application Slim définit un message qui sera disponible dans les modèles d'affichage de la requête en cours.
Dans cet exemple, le message sera disponible dans le modèle par la variable `flash['info']`.

    <?php
    $app->flashNow('info', 'Votre carte de crédit a expiré');
