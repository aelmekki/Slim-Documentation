---
title: Installation
status: live
---

### Installation avec Composer

Installez *composer* dans votre projet:

    curl -s https://getcomposer.org/installer | php

Créez un fichier `composer.json` à la racine de votre projet:

    {
        "require": {
            "slim/slim": "2.*"
        }
    }

Installez *Slim* via composer:

    php composer.phar install

Ajoutez cette ligne dans le fichier `index.php` de votre application:

    <?php
    require 'vendor/autoload.php';

### Installation Manuelle

Téléchargez et extrayez *The Slim Framework* dans le répertoire de votre projet puis, dans le fichier `index.php` de votre application faites un `require` de Slim. 
Vous devrez aussi enregistrer l'autoloader de Slim.

    <?php
    require 'Slim/Slim.php';
    \Slim\Slim::registerAutoloader();
