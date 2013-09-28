---
title: Niveaux de Log
status: live
---

<div class="alert alert-info">
    <strong>Attention!</strong> Utilisez la constante <code>\Slim\Log</code> pour paramétrer le niveau de log plutôt que les valeurs en entier (dans le sens integer).
</div>

L'objet de log de l'application Slim va traiter ou ignorer les messages enregistrés sur la base de son réglage de niveau de log. lorsque vous invoquez les méthodes des objets de log, vous faites l'attribution d'un niveau au message automatiquement. Les niveaux de log disponibles sont les suivants:

\Slim\Log::EMERGENCY
: Niveau 1

\Slim\Log::ALERT
: Niveau 2

\Slim\Log::CRITICAL
: Niveau 3

\Slim\Log::ERROR
: Niveau 4

\Slim\Log::WARN
: Niveau 5

\Slim\Log::NOTICE
: Niveau 6

\Slim\Log::INFO
: Niveau 7

\Slim\Log::DEBUG
: Niveau 8

Seuls les messages qui ont un niveau inférieur (ou égal) au niveau de l'objet de log seront traités. Par exemple, si le niveau de l'objet de log est `\Slim\Log::WARN` (5), alors il ignorera les messages de niveau `\Slim\Log::DEBUG`, `\Slim\Log::INFO` et `\Slim\Log::NOTICE`, mais traitera les messages de niveau `\Slim\Log::WARN`, `\Slim\Log::ERROR` ou encore `\Slim\Log::CRITICAL` et au dessus.

### Comment définir le niveau de log

    <?php
    $app->log->setLevel(\Slim\Log::WARN);

Vous pouvez le définir pendant l'instanciation aussi:

    <?php
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::WARN
    ));
