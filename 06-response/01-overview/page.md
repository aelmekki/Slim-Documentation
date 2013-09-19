---
title: Généralités sur la réponse
status: live
---

Chaque instance d'application Slim dispose d'un objet response. Cet objet response est une abstraction de vos réponses HTTP retournées au client HTTP par l'application Slim. De plus, chaque application Slim inclue une réponse par défaut (un objet response), la classe `\Slim\Http\Response` est idempotente; vous pouvez l'instancier quand vous voulez (dans un middleware ou ailleurs) sans affecter l'application. Vous pouvez obtenir une référence de l'objet response de slim par:

    <?php
    $app = new \Slim\Slim();
    $app->response;

Une réponse HTTP a 3 propriétés primaires:

* Status
* Header
* Body

L'objet response fourni des méthodes d'aide, décrites par la suite, qui vous aident à interagir avec ces propriétés de réponses HTTP. L'objet par défaut response retournera un **200 OK** avec un type de contenu **text/html**.
