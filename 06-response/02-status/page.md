---
title: Statut de la réponse
status: live
---

La réponse HTTP retournée au client aura un code de statut qui indique le type de répons (par exemple 200 OK, 400 Bad Request, or 500 Server Error). Vous pouvez utiliser l'objet response de Slim pour assigner ce statut de réponse HTTP comme cela:

    <?php
    $app->response->setStatus(400);

Vous avez seulement besoin d'assigner le statut de l'objet response si vous voulez retourner une réponse qui *n'est pas* une 200 OK. Vous pouvez connaître le statut courant, tout simplement en invoquant la même méthode, mais sans argument, comme cela:

    <?php
    $status = $app->response->getStatus();
