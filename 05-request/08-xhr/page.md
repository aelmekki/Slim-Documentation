---
title: XMLHttpRequest
status: live
---

Quand vous utilisez un framework comme MooTools ou jQuery pour exécuter un XMLHttpRequest, ce XMLHttpRequest va, en général, être envoyé avec un header HTTP **X-Requested-With**. L'application Slim va détecter ce header **X-Requested-With** et marquer la requête comme tel. Si pour certaines raisons, un XMLHttpRequest ne peut pas être envoyée avec le header **X-Requested-With**, vous pouvez forcer Slim à considérer que c'est une requête HTTP de type XMLHttpRequest en appliquant un paramètre (GET, POST ou PUT) dans la requête HTP nommé “isajax” avec une valeur vraie.

Utilisez les méthodes `isAjax()` ou `isXhr()` de l'objet request pour savoir si la requête courante est une requête XHR/Ajax:

    <?php
    $isXHR = $app->request->isAjax();
    $isXHR = $app->request->isXhr();
