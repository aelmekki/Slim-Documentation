---
title: Généralités
status: live
---

Une application Slim fournit un objet de log qui écrit des données dans une sortie spécifique. Cette écriture de données est faite par un log writer.

### Comment "logger" des données

Pour logger des données dans une application Slim, obtenez une référence à l'objet de log:

    <?php
    $log = $app->log;

Cet objet fournit les interfaces PSR-3 suivantes:

    $app->log->debug(mixed $object);
    $app->log->info(mixed $object);
    $app->log->notice(mixed $object);
    $app->log->warning(mixed $object);
    $app->log->error(mixed $object);
    $app->log->critical(mixed $object);
    $app->log->alert(mixed $object);
    $app->log->emergency(mixed $object);

Chaque méthode de l'objet de log accepte un argument mixte. L'argument est habituellement une chaîne de caractères, mais il peut être n'importe quoi. L'objet de log va passer l'argument à son log writer. C'est le job du log writer d'écrire arbitrairement l'entrée dans la destination appropriée.
