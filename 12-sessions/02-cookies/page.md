---
title: Stockage de Cookies de Session
status: live
---

Vous pouvez également utiliser le middleware `\Slim\Middleware\SessionCookie` pour conserver les données de session dans des cookies HTTP cryptés et hachés. Pour activer le middleware de cookies de session, ajoutez le middleware `\Slim\Middleware\SessionCookie` à votre application Slim:

    <?php
    $app = new Slim();
    $app->add(new \Slim\Middleware\SessionCookie(array(
        'expires' => '20 minutes',
        'path' => '/',
        'domain' => null,
        'secure' => false,
        'httponly' => false,
        'name' => 'slim_session',
        'secret' => 'CHANGEZ_MOI',
        'cipher' => MCRYPT_RIJNDAEL_256,
        'cipher_mode' => MCRYPT_MODE_CBC
    )));

Le deuxième argument est optionnel, il est montré ici pour que vous puissiez voir les paramètres de middleware par défaut. Le middleware de cookies de session fonctionne de manière transparente avec la superglobale `$_SESSION`  de sorte que vous puissiez facilement migrer vers ce middleware de stockage avec sans modification du code de votre application.

Si vous utilisez le middleware de cookie de session, vous n'avez PAS besoin de démarrer une session PHP native. La superglobale `$_SESSION` sera toujours disponible, et il sera persisté dans un cookie HTTP via la couche de middleware plutôt que par la gestion des sessions native de PHP.

Rappelez-vous, les cookies HTTP sont, par nature, limités à 4 kilo-octets de données. Si vos données de session cryptés dépassent cette longueur, vous devriez plutôt utiliser les sessions natives de PHP ou un gestionnaire de sessions alternatif.

<div class="alert">
    <strong>A NOTER:</strong> Le stockage de données de sessions côté-client n'est pas recommandé si vous travaillez avec des informations sensibles, même en utilisant le middleware de cookies de sessions chiffrés.
	Si vous devez stocker des informations sensibles, vous devriez chiffrer et stocker les informations de sessions sur votre serveur.
</div>
