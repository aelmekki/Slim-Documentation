---
title: Les Cookies 
status: live
---

### Récupérer les cookies

Une application Slim va automatiquement parser les cookies envoyées avec la requête HTTP. Vous pouvez récupérer les valeurs de cookies avec la méthode d'aide `getCookie()` de Slim, comme cela:

    <?php
    $app = new \Slim\Slim();
    $foo = $app->getCookie('foo');

Seuls les cookies envoyés avec la requête HTTP courante sont accessibles avec cette méthode. Si vous assignez un cookie durant la requête courante, il ne sera pas accessible avec cette méthode avant la requête. Vous pouvez aussi récupérer la liste complète des cookies de la requête HTTP via l'objet \Slim\Http\Request:

    <?php
    $cookies = $app->request->cookies;

Cela va retourner une instance de \Slim\Helper\Set dont vous pouvez utiliser l'interface pour inspecter les cookies.

### Chiffrage de cookie

Vous pouvez, optionnellement, choisir de chiffre vos cookies stockés chez le client HTTP avec le paramètre `cookies.encrypt` de Slim. Quand ce paramètre est `true`, tous les cookies seront chiffrés en utilisant la clé et la méthode définies.

C'est aussi simple que cela. Les cookies seront chiffrés automatiquement avant d'être envoyés chez le client. Ils seront aussi déchiffrés sur demande quand vous les demandez avec `\Slim\Slim::getCookie()`.
