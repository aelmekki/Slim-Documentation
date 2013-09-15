---
title: Présentation de la configuration
status: live
---

Il y a deux façons de configurer une application Slim. L'une durant l'instantiation de l'application Slim et l'autre, après l'instantation.
Tous les paramètres peuvent êtres appliqués au moment de l'instantiation en passant au constructeur de Slim un tableau associatif. Tous les paramètres peuvent être retrouvés et modifiés après l'instantation, cependant, certains d'entre eux ne peuvent se paramétrer simplement en utilisant la méthode config d'une instance de Slim. Pour ces cas, une démonstration sera faite plus bas.
Avant de lister les paramètres disponibles, je voudrai expliquer comment vous pouvez définir et inspecter les paramètres avec votre application Slim.

### Pendant l'Instanciation

Pour définir les paramètres dans l'instancation, passez un tabeau associatif dans le constructeur de Slim

    <?php
    $app = new Slim(array(
        'debug' => true
    ));

### Après l'Instantiation

Pour définir des paramètres après l'instanciation, en général, il est possible d'utiliser la méthode config de l'application; Le premier argument est le nom du paramètre et le second est la value que vous désirer lui affecter.

    <?php
    $app->config('debug', false);

Vous pouvez aussi définir de multiples paramètres en une fois, en utilisant un tableau associatif:

    <?php
    $app->config(array(
        'debug' => true,
        'templates.path' => '../templates'
    ));

Pour récuperer la valeur d'un paramètre, vous pouvez aussi utiliser la méthode config de l'instance de votre application; Pour ce cas, il ne faut passer qu'un argument - le nom du paramètre que vous voulez inspecter. Si le paramètre n'existe pas, la méthode retournera `null`.

    <?php
    $settingValue = $app->config('templates.path'); //returns "../templates"

Vous n'êtes pas limités aux paramètres de base; vous pouvez aussi défnir les votres
