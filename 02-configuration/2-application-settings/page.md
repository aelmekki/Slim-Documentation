---
title: Paramètres de l'application
status: live
---

### mode

C'est un identifiant pour le mode de l'application. Ce mode n'affecte en rien les fonctionalités de l'application Slim. 
En fait, le mode vous sert seulement si vous voulez exécuter des morceaux de code spéciaux en fonction de celui-ci, cela est possible grâce à la méthode `configMode()` de l'application.
Le mode de l'application est déclaré à l'instanciation, que cela soit avec une variable d'environement ou avec un argument passé dans le constructeur. Il ne peut plus être changé après. La valeur n'a pas d'importance et peut-être n'importe quoi - "development", "test" et "production" sont des exemples typiques, mais n'hésitez pas à mettre une valeur personalisée (pourquoi pas "foo" ou "bar").

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'development'
    ));

Type du paramètre
: string

Valeur par défaut
: "development"

### debug

<div class="alert alert-info">
    <strong>Attention!</strong> Slim traduit les erreurs en instances d'`ErrorException`.
</div>

Si le mode débogage est activé, Slim va utiliser son système de gestion d'erreur pour afficher des informations de diagnostique sur les exceptions qui ne sont pas attrapées / catchées.
En revanche, si ce mode est désactivé, Slim invoquera votre gestionnaire d'erreur personalisé en lui passant ces mêmes exceptions comme premier argument.

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

Type du paramètre
: boolean

Valeur par défaut
: true

### log.writer

Utiliser un logueur pour pouvoir loguer des messages dans les sorties apropriées. Par défaut, le logueur de Slim va écrire les messages dans `STDERR`. Si vous voulez utiliser un logueur personalisé, il doit simplement implémenter cette interface: 

    public write(mixed $message, int $level);

La méthode `write()` est celle qui gère l'envoie de message de log (pas forcément une chaine de caractères) dans la bonne sortie (par exemple, un fichier texte, une base de données ou encore un web service).

Pour utiliser un logueur personalisé après l'instanciation, vous devez directement modifier celui de Slim et utiliser sa méthode `setWriter()`.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'log.writer' => new \My\LogWriter()
    ));

    // Après instanciation
    $log = $app->getLog();
    $log->setWriter(new \My\LogWriter());

Type du paramètre
: mixed

Valeur par défaut
: \Slim\LogWriter

### log.level

<div class="alert alert-info">
    <strong>Attention!</strong> Utilisez les constantes définies dans `\Slim\Log` plutôt que les valeures (les entiers).
</div>

Slim dispose de ces différents niveaux de log:

* \Slim\Log::EMERGENCY
* \Slim\Log::ALERT
* \Slim\Log::CRITICAL
* \Slim\Log::ERROR
* \Slim\Log::WARN
* \Slim\Log::NOTICE
* \Slim\Log::INFO
* \Slim\Log::DEBUG

Le paramètre `log.level` de l'application détermine quel message sera affiché et quel message sera ignoré.
Par exemple, si le `log.level` vaut `\Slim\Log::INFO`, les messages de debug seront ignorés, alors que les messages du type info, warn, error, et fatal seront logués.

Pour changer ce paramètre après l'instanciation, vous devez accéder au logueur de Slim et utiliser la méthode `setLevel()`.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::DEBUG
    ));

    // Après l'instanciation
    $log = $app->getLog();
    $log->setLevel(\Slim\Log::WARN);

Type du paramètre
: integer

Valeur par défaut
: \Slim\Log::DEBUG

### log.enabled

Cela active ou désactive le logueur de Slim. Pour changer ce paramètre après l'instanciation, il faut accéder au logueur de Slim et utiliser directement sa méthode `setEnabled()`.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'log.enabled' => true
    ));

    // Après l'instanciation
    $log = $app->getLog();
    $log->setEnabled(true);

Type du paramètre
: boolean

Valeur par défaut
: true

### templates.path

Le chemin, relatif ou absolu, jusqu'au dossier qui contient vos templates d'application Slim.
Ce chemin est utilisé par la vue de l'application Slim (View) pour trouver et utiliser les templates.

Pour changer ce paramètre après l'instanciation, vous devez accéder à la vue de Slim directement et utiliser sa méthode `setTemplatesDirectory()`.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'templates.path' => './templates'
    ));

    // Après l'instanciation
    $view = $app->view();
    $view->setTemplatesDirectory('./templates');

Type du paramètre
: string

Valeur par défaut
: "./templates"

### view

La classe View, plus précisément son instance, utilisé par l'application Slim. Pour changer ce paramètre après l'instanciation, il vous faut utiliser la méthode `view()`de l'application Slim.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'view' => new \My\View()
    ));

    // Après l'instanciation
    $app->view(new \My\View());

Type du paramètre
: string|\Slim\View

Valeur par défaut
: \Slim\View

### cookies.encrypt

Détermines si l'application Slim doit chiffrer les cookies HTTP ou non.

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true
    ));

Type du paramètre
: boolean

Valeur par défaut
: false

### cookies.lifetime

Paramètre la durée de vie d'un cookie HTTP créé par l'application Slim. Si c'est un entier, il doit être un timestamp UNIX valide, il représente la date à laquelle le cookie expire.
Si c'est une chaine de caractèr, il est converti par la fonction `strtotime()` afin d'avoir un timestamp UNIX valide pour savoir quand le cookie expire.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.lifetime' => '20 minutes'
    ));

    // Après l'instanciation
    $app->config('cookies.lifetime', '20 minutes');

Type du paramètre
: integer|string

Valeur par défaut
: "20 minutes"

### cookies.path

Détermine le chemin du cookie HTTP si aucun n'a déjà été spécifié quand la méthode `setCookie()`, ou encore `setEncryptedCookie()`, a été utilisée.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.path' => '/'
    ));

    // Après l'instanciation
    $app->config('cookies.path', '/');

Type du paramètre
: string

Valeur par défaut
: "/"

### cookies.domain

Détermine le dommaine du cookie HTTP si aucun n'a déjà été spécifié quand la méthode `setCookie()`, ou encore `setEncryptedCookie()`, a été utilisée.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.domain' => 'domain.com'
    ));

    // Après l'instanciation
    $app->config('cookies.domain', 'domain.com');

Type du paramètre
: string

Valeur par défaut
: null

### cookies.secure

Détermine si le cookie doit être délivré seulement en HTTPS ou non. Ce paramètre peut être changé lors de l'appel à la méthode `setCookie()`de Slim ou encore `setEncryptedCookie()`.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.secure' => false
    ));

    // Après l'instanciation
    $app->config('cookies.secure', false);

Type du paramètre
: boolean

Valeur par défaut
: false

### cookies.httponly

Détermine si le cookie doit être délivré seulement en HTTP ou non. Ce paramètre peut être changé lors de l'appel à la méthode `setCookie()`de Slim ou encore `setEncryptedCookie()`.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.httponly' => false
    ));

    // Après l'instanciation
    $app->config('cookies.httponly', false);

Type du paramètre
: boolean

Valeur par défaut
: false

### cookies.secret_key

La clé secrète utilisée pour chiffrer les cookies. Vous devez changer ce paramètre si vous utilisez des cookies HTTP chiffrés dans votre application Slim.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.secret_key' => 'secret'
    ));

    // Après l'instanciation
    $app->config('cookies.secret_key', 'secret');

Type du paramètre
: string

Valeur par défaut
: "CHANGE_ME"

### cookies.cipher

Le type de chiffrement utilisé pour le cookie HTTP. Voir [chiffrements disponibles](http://php.net/manual/fr/mcrypt.ciphers.php).

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.cipher' => MCRYPT_RIJNDAEL_256
    ));

    // Après l'instanciation
    $app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);

Type du paramètre
: integer

Valeur par défaut
: MCRYPT_RIJNDAEL_256

### cookies.cipher_mode

Le mode de chiffrement utilisé pour le cookie HTTP. Voir [modes de chiffrements disponibles](http://php.net/manual/fr/mcrypt.ciphers.php).

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

    // Après l'instanciation
    $app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);

Type du paramètre
: integer

Valeur par défaut
: MCRYPT_MODE_CBC

### http.version

Par défaut, Slim retourne une réponse HTTP/1.1 au client. Il faut utiliser ce paramètre si vous voulez retourner une réponse HTTP/1.0. Cela peut-être utile si vous utilisez PHPFog ou un serveur nginx qui communique avec des proxies au lieu de répondre directement au client HTTP.

    <?php
    // Pendant l'instanciation
    $app = new \Slim\Slim(array(
        'http.version' => '1.1'
    ));

    // Après l'instanciation
    $app->config('http.version', '1.1');

Type du paramètre
: string

Valeur par défaut
: "1.1"
