---
title: Sessions natives
status: live
---

Une application Slim ne force en rien son modèle de sessions. Si vous préférez utiliser une session PHP, vous devez configurer et démarrer une session de PHP native avec `session_start()` avant d'instancier l'application Slim.

Vous devez également désactiver le limiteur de cache de sessions PHP pour que PHP n'envoie pas d'en-têtes d'expiration du cache qui seraient contradictoires avec la réponse HTTP. Vous pouvez désactiver ce limiteur avec:

    <?php
    session_cache_limiter(false);
    session_start();
