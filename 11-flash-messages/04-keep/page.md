---
title: "Flash" persistant
status: live
---

Cette méthode demande à l'application Slim de garder un message "flash" existant de la requête précédente pour qu'il soit disponible dans la requête suivante. Cette méthode est utile pour garder des messages persistants dans les redirections HTTP par exemple.

    <?php
    $app->flashKeep();
