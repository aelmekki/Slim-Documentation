---
title: Généralités sur les requêtes
status: live
---

Chaque instance d'application Slim dispose d'un objet requête. Cet objet est une représentation de la requête HTTP courante et vous permet de facilement interagir avec les variables d'environnement Slim. De plus, chaque application Slim inclue un objet requête par défaut, la classe `\Slim\Http\Request` est idempotente; vous pouvez instancier la classe quand vous voulez (dans un middleware ou ailleurs dans l'application) sans affecter l'application. Vous pouvez obtenir une référence à l'objet requête de l'application Slim comme cela:

    <?php
    // Retourne une instance de \Slim\Http\Request
    $request = $app->request;
