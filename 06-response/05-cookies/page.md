---
title: Cookies
status: live
---

L'application Slim fournit des méthodes d'aide pour envoyer des cookies dans les réponses HTTP.

### Assigner un cookie

Cet exemple montre comment utiliser la méthode `setCookie()` de l'application Slim pour créer un cookie HTTP à envoyer dans une réponse HTTP:

    <?php
    $app->setCookie('foo', 'bar', '2 days');

Cela crée un cookie HTTP avec le nom "foo" et la valeur "bar" qui expire dans 2 jours à partir d'aujourd'hui. Vous pouvez aussi fournir des propriétés en plus, dont le chemin, le domaine, sécuriser et des paramètres httponly. La méthode `setCookie()` utilise la même signature que la méthode native de PHP `setCookie()`.

    <?php
    $app->setCookie(
        $name,
        $value,
        $expiresAt,
        $path,
        $domain,
        $secure,
        $httponly
    );

### Chiffrer les cookies

Vous pouvez demander à Slim de chiffrer les cookies de réponse en mettant le paramètre d'application `cookies.encrypt` à `true`. Quand ce paramètre est `true`, Slim va chiffrer automatiquement les cookies de réponse avant de les envoyer au client HTTP.

Voici les paramètres de l'application Slim utilisés pour le chiffrage de cookie:

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true,
        'cookies.secret_key' => 'ma_clé_secrète',
        'cookies.cipher' => MCRYPT_RIJNDAEL_256,
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

### Supprimer un cookie

Vous pouvez supprimer un cookie en utilisant la méthode `deleteCookie()` de l'application Slim. Cela supprime le cookie du client HTTP avant la prochaine requête HTTP. Cette méthode accepte la même signature que `setCookie()` *sans* l'argument `$expires`. Seul le premier argument est requis.

    <?php
    $app->deleteCookie('foo');

Si vous devez aussi spécifier le chemin et le domaine:

    <?php
    $app->deleteCookie('foo', '/', 'foo.com');

Vous pouvez aussi spécifier les propriétés secure et httponly:

    <?php
    $app->deleteCookie('foo', '/', 'foo.com', true, true);
