---
title: Activer le Logging
status: live
---

L'objet de log de Slim propose les méthodes publiques suivantes pour activer ou désactiver le logging durant l'exécution:

    <?php
    //Activer le logging
    $app->log->setEnabled(true);

    //Désactiver le logging
    $app->log->setEnabled(false);

Vous pouvez activer ou désactiver les logs de l'application directement à instanciation comme cela:

    <?php
    $app = new Slim(array(
        'log.enabled' => true
    ));

Si les logs sont désactivés, le writer ignorera tous les messages jusqu'à ce qu'il soit activé.