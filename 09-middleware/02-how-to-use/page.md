---
title: Comment utiliser un Middleware
status: live
---

Utilisez la méthode `add()` d'une application Slim pour ajouter un nouveau middleware à une application. Un nouveau middleware va suivre le dernier middleware ajouté, ou l'application Slim en elle-même si aucun middleware n'a encore été ajouté.

### Exemple de Middleware

Ce middleware d'exemple va mettre en majuscule le corps de la réponse HTTP de l'application Slim.

    <?php
    class AllCapsMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            // Récupérer la référence de l'application
            $app = $this->app;

            // Exécuter les middleware internes et Slim.
            $this->next->call();

            // Mettre en majuscule la réponse
            $res = $app->response;
            $body = $res->getBody();
            $res->setBody(strtoupper($body));
        }
    }

### Ajouter un Middleware

    <?php
    $app = new \Slim\Slim();
    $app->add(new \AllCapsMiddleware());
    $app->get('/foo', function () use ($app) {
        echo "Hello";
    });
    $app->run();

La méthode `add()` de Slim accepte un seul argument: une instance de middleware. Si l'instance de middleware nécessite une configuration spéciale, elle doit implémenter son propre constructeur pour être configurée avant d'être ajoutée à une application Slim.

Quand l'exemple d'application Slim ci-dessus est exécuté, le corps réponse HTTP sera un "HELLO".
