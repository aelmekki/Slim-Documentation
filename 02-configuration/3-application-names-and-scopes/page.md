---
title: Noms d'applications et portées
status: live
---

Lorsque vous faites une application Slim, vous allez pouvoir utiliser différentes portées dans votre code (par exemple portée globale et portée limitée à une fonction).
D'ailleurs, vous aurez surement besoin d'une référence de votre application Slim dans chacune de ces portées. 
Il y a plusieurs façons de faire cela :

* Utiliser des noms d'applications avec la méthode statique `getInstance()` de Slim
* Récuperer une instance de l'application dans une fonction en utilisant le mot-clé `use`

### Noms d'applications

Chaque application Slim peut avoir un nom. **C'est optionel**. Les noms vous aident à retrouver une référence à une instance d'application Slim, et cela quelle que soit la portée du code dans lequel vous êtes. 
Voici comment on définit et récupère un nom d'application:

    <?php
    $app = new \Slim\Slim();
    $app->setName('foo');
    $name = $app->getName(); // "foo"

### Résolution de portée

Comment récupérer une référence de votre application Slim? L'exemple suivant montre comment obtenir une référence à une application Slim dans une fonction de routage. 
La variable `$app` est utilisée dans une portée globale pour définir les routes HTTP GET. 
Cependant, cette même variable `$app` est aussi nécessaire dans la fonction de rappel appelée pour le rendu d'un template.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        $app->render('foo.php'); // <-- ERROR
    });

Cet exemple ne fonctionne pas car la variable `$app` est indisponible dans la fonction de rappel.

#### Résoudre le problème

Nous pouvons injecter la variable `$app` dans la fonction de rappel grâce au mot-clé `use`:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $app->render('foo.php'); // <-- SUCCESS
    });

#### Récupération par le nom

Il est aussi possible d'utiliser la fonction statique `getInstance() de Slim:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', 'foo');
    function foo() {
        $app = Slim::getInstance();
        $app->render('foo.php');
    }
