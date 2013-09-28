---
title: "Flash" pour le suivant
status: live
---

La méthode `flash()` de l'application Slim définit un message qui sera disponible dans les modèles d'affichage de la prochaine requête.
Dans cet exemple, le message sera disponible dans le modèle par la variable `flash['error']`.

    <?php
    $app->flash('error', "L'adresse email est requise");
