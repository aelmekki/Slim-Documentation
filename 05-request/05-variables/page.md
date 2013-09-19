---
title: Variables de requête
status: live
---

Une requête HTTP peut avoir des variables associées (à ne pas confondre avec les variables de la route). Les variables GET, POST, PUT envoyées avec la requête HTTP en cours sont exposées via l'objet `request` de l'application Slim.

Si vous voulez rapidement récupérer une variable de requête sans tenir compte de son type, utilisez la méthode `params()` de request:

    <?php
    $app = new \Slim\Slim();
    $paramValue = $app->request->params('paramName');

La méthode `params()` va premièrement rechercher les variables PUT, puis POST et enfin GET. Si aucune variable n'est trouvée, `null` est renvoyé. Si vous voulez un type précis de variable, vous pouvez utiliser ces méthodes:

    <?php
    //variable GET 
    $paramValue = $app->request->get('paramName');

    //variable POST 
    $paramValue = $app->request->post('paramName');

    //variable PUT 
    $paramValue = $app->request->put('paramName');

Si une variable n'existe pas, chaque méthode ci-dessus retournera `null`. Vous pouvez aussi appeler une de ces fonctions sans argument pour obtenir un tableau de toutes les variables pour un type donné:

    <?php
    $allGetVars = $app->request->get();
    $allPostVars = $app->request->post();
    $allPutVars = $app->request->put();
