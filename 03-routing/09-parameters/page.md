---
title: Les paramètres de route
status: live
---

Vous pouvez intégrer des paramètres dans vos URIs. Par exemple, j'ai deux paramètres dans ma route, “:one” et “:two”.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:one/:two', function ($one, $two) {
        echo "Le premier paramètre est " . $one;
        echo "Le second paramètre est " . $two;
    });

Pour créer un paramètre URI, ajoutez “:” en préfix au nom du paramètre dans le patron d'URI. Quand la route correspond à la requête courante, la valeur de chaque paramètre de la route est extraite de la requête HTTP et fournie à la fonction de rappel dans l'ordre d'apparition.

### Paramètre de route générique

Vous pouvez aussi utiliser des paramètres de route génériques. En faisant cela, l'application va capturer un ou plusieurs segments de l'URI qui correspondent au patron de la route et les renvoyer dans un tableau.
Un paramètre générique est identifié par un suffixe “+”; il fonctionne, cela-dit, exactement comme un paramètre normal expliqué ici. Voici un exemple:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name+', function ($name) {
        // Faire quelque chose
    });

Quand vous utilisez cet exemple d'application avec une URI qui est “/hello/Josh/T/Lockhart”, l'argument de la fonction de rappel, `$name`, sera `array('Josh', 'T', Lockhart')`.

### Segments de route optionnels

<div class="alert alert-warning">
    <strong>Attention!</strong> Les segments de routes optionnels sont expérimentaux. Ils ne doivent être utilisés que dans la manière décrite ci-dessous.
</div>

Vous pouvez aussi avoir des paramètres de route optionnels. C'est l'idéal pour utiliser une route qui va chercher les archives d'un blog. Pour déclarer ces paramètres optionnels, spécifiez votre patron de route comme cela:

    <?php
    $app = new Slim();
    $app->get('/archive(/:year(/:month(/:day)))', function ($year = 2010, $month = 12, $day = 05) {
        echo sprintf('%s-%s-%s', $year, $month, $day);
    });

Chaque ségment de route est facultatif. Cette route fonctionnera les requêtes HTTP suivantes: 

* /archive
* /archive/2010
* /archive/2010/12
* /archive/2010/12/05

Si un segment de route n'est pas présent dans la requête HTTP, la valeur par défaut dans la signature de la fonction de rappel sera utilisée à la place.

Actuellement, vous pouvez utiliser les segments de route facultatif dans des situations comme l'exemple ci-dessus, où chaque segment est optionnel. Vous allez peut-être trouver cette fonctionnalité instable lorsqu'elle sera utilisée dans des scénarios différents de l'exemple ci-dessus.
