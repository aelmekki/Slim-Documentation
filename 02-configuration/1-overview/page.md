---
title: Présentation de la configuration
status: live
---

Il y a deux façons de configurer une application Slim. L'une durant l'instanciation de l'application, l'autre, après l'instanciation.
Tous les paramètres peuvent être appliqués au moment de l'instanciation, en passant au constructeur de Slim un tableau associatif. 
Tous ces paramètres peuvent d'ailleurs être retrouvés et modifiés après l'instanciation, cependant, certains d'entre eux ne peuvent pas  se paramétrer de façon simple en utilisant la méthode config de Slim. 
Pour ces cas, une démonstration sera faite.
Avant de lister les paramètres disponibles, je vais expliquer comment vous pouvez définir et inspecter les paramètres avec votre application Slim.

### Pendant l'Instanciation

Pour définir les paramètres à l'instanciation, passez un tableau associatif dans le constructeur de Slim:

    <?php
    $app = new Slim(array(
        'debug' => true
    ));

### Après l'Instantiation

Pour définir des paramètres après l'instanciation, en général, il est possible d'utiliser la méthode config de l'application; le premier argument est le nom du paramètre et le second est la valeur que vous désirez lui affecter.

    <?php
    $app->config('debug', false);

Vous pouvez aussi définir plusieurs paramètres en une fois, en utilisant un tableau associatif:

    <?php
    $app->config(array(
        'debug' => true,
        'templates.path' => '../templates'
    ));

Pour récupérer la valeur d'un paramètre, vous pouvez aussi utiliser la méthode config de l'instance de votre application; pour ce cas, il ne faut passer qu'un argument: le nom du paramètre que vous voulez inspecter. Si le paramètre n'existe pas, la méthode retournera `null`.

    <?php
    $settingValue = $app->config('templates.path'); //returns "../templates"

Vous n'êtes pas limité aux paramètres de base; vous pouvez aussi définir les vôtres.
