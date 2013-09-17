---
title: Conditions de Routage 
status: live
---

Slim vous offre le possibilité de créer des paramètres qui agissent comme des conditions de routage. Si les paramètres ne sont pas validés, le routage ne s'effectue pas. Par exemple, si vous avez besoin d'une route avec un segment qui doit être une date à 4 chiffres, vous pouvez forcer cette condition comme cela:

    <?php
    $app = new \Slim\Slim();
    $app->get('/archive/:year', function ($year) {
        echo "Vous visionnez les archives de l'année $year";
    })->conditions(array('year' => '(19|20)\d\d'));

Utilisez la méthode `conditions()` de l'objet Route. Le premier et dernier argument est un tableau associatif, dont, les clés sont des paramètres de votre route (dans l'exemple *year*) et les valeurs des expressions régulières.

### Condition de routage à l'échelle de l'application

Si plusieurs de vos routes (dans une applications Slim) ont les mêmes paramètres et utilisent les mêmes conditions, vous pouvez définir des conditions de routage à l'échelle de l'application, comme cela:

    <?php
    \Slim\Route::setDefaultConditions(array(
        'firstName' => '[a-zA-Z]{3,}'
    ));

Définissez ces conditions de routage d'application avant de définir vos routes. Quand vous définissez une route, elle va automatiquement s'attribuer les conditions de routage définies avec `\Slim\Route::setDefaultConditions()`.
Si pour quelque raison que ce soit, vous avez besoin de retrouver vos conditions de routage d'application, vous pouvez les récupérer avec `\Slim\Route::getDefaultConditions()`. Cette méthode statique retourne un tableau qui contient les conditions exactement telles qu'elles ont été définies au départ.

Vous pouvez surcharger une condition de routage par défaut en redéfinissant la condition de routage lorsque vous définissez la route, comme ci-dessous:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:firstName', $callable)
        ->conditions(array('firstName' => '[a-z]{10,}'));

Vous pouvez apprendre des nouvelles conditions à une route donnée comme cela:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:firstName/:lastName', $callable)
        ->conditions(array('lastName' => '[a-z]{10,}'));
