---
title: Réécriture d'URL
status: live
---

Je vous encourage (grandement) à utiliser un serveur web qui gère la réécriture d'URL; cela vous permet de profiter d'URLs propres, compréhensibles par l'homme, avec votre application Slim. Pour activer la réécriture d'URL, vous devez utiliser les outils appropriés fournis par votre serveur web, qui vont transmettre toutes les requêtes HTTP à un fichier PHP dans lequel vous instanciez et exécutez votre application Slim. Les exemples suivants sont le strict minimum d'une configuration pour Apache avec mod_php et nginx. Ils ne sont pas censés fonctionner en production mais suffisent à vous montrer les principes. Pour en savoir plus sur le déploiement sur un serveur, vous pouvez lire <http://www.phptherightway.com>.

### Apache et mod_rewrite

Voici un exemple de structure de dossiers:

    /path/www.mysite.com/
        public_html/ <-- Racine!
            .htaccess
            index.php <-- J'instancie Slim ici!
        lib/
            Slim/ <-- Les fichiers de Slim (librairie) sont ici!

L'**.htaccess** dans le dossier contient:

    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [QSA,L]

Vous aurez aussi besoin d'une directive de répertoire pour activer le fichier **.htaccess** et autoriser la directive **RewriteEngine** à être utilisée.
C'est, parfois, fait par le fichier **httpd.conf**, mais c'est souvent une bonne idée de limiter la directive à seulement votre hôte virtuel en la mettant (la directive) dans votre bloc de configuration **VirualHost**. C'est généralement fait comme cela:

    <VirtualHost *:80>
        ServerAdmin me@mysite.com
        DocumentRoot "/path/www.mysite.com/public_html"
        ServerName mysite.com
        ServerAlias www.mysite.com

        #ErrorLog "logs/mysite.com-error.log"
        #CustomLog "logs/mysite.com-access.log" combined

        <Directory "/path/www.mysite.com/public_html">
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
    </VirtualHost>

Le résultat? Apache va envoyer toutes les requêtes pour des fichiers qui n'existent pas vers le script **index.php** où j'instancie et exécute mon application Slim. Avec la réécriture d'URL activée, et en considérant l'application Slim suivante, vous pouvez accéder à la route de l'application par “/foo” plutôt que par “/index.php/foo”.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        echo "Foo!";
    });
    $app->run();

### nginx

Nous allons utiliser la même structure exemple que précédemment, mais avec nginx notre configuration est faite dans **nginx.conf**.

    /path/www.mysite.com/
        public_html/ <-- Racine!
            index.php <-- J'instancie Slim ici!
        lib/
            Slim/ <-- Les fichiers de Slim (librairie) sont ici!

Voici un extrait d'un fichier **nginx.conf** dans lequel nous utilisons la directive **try_files** pour fournir le fichier s'il existe (bien pour les fichiers statics comme les images, les css, le js et autres) et sinon, transférer la requête au fichier **index.php**.

    server {
        listen       80;
        server_name  www.mysite.com mysite.com;
        root         /path/www.mysite.com/public_html;

        try_files $uri /index.php;

       	# cela ne fera que passer index.php au processus FastCGI ce qui est généralement sûr
		# mais considère que l'ensemble du site est géré par Slim.
        location /index.php {
            fastcgi_connect_timeout 3s;     # la valeur par défaut de 60s is simplement trop longue
            fastcgi_read_timeout 10s;       # la valeur par défaut de 60s is simplement trop longue
            include fastcgi_params;
            fastcgi_pass 127.0.0.1:9000;    # considère que vous exécutez php-fpm localement sur le port 9000
        }
    }

Une majorité des installations auront un fichier **fastcgi_params** par défaut qu'il suffit d'inclure comme montré ici. Certaines configurations n'ont pas le paramètre **SCRIPT_FILENAME**. Vous devez vous assurer que vous incluez ce paramètre, sinon vous allez vous retrouver avec une erreur du type "No input file specified" par le processus fastcgi. Cela peut être fait directement dans le bloc de localisation ou simplement ajouté aux paramètres du fichier **fastcgi_params**. Quoi qu'il en soit, cela ressemble à cela:

    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;

### Sans réécriture d'URL

Slim fonctionne sans réécriture d'URL. Dans ce scénario, vous devez inclure le nom du fichier PHP, dans lequel vous instanciez et exécutez l'application Slim, dans votre ressource URL. Par exemple, en considérant l'application suivante (définie dans **index.php**, à la racine de votre hôte):

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        echo "Foo!";
    });
    $app->run();

Vous pouvez accéder à la route spécifiée par “/index.php/foo”. Si la même application est définie dans un sous répertoire, par exemple blog/, vous pouvez accéder la route par “/blog/index.php/foo”.
