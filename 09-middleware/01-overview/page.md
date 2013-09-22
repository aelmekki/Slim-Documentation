---
title: Généralités sur les Middlewares
status: live
---

The Slim Framework implémente une version du protocole Rack. En conséquence, une application Slim peut avoir  des middlewares qui peuvent inspecter, analyser, ou de modifier l'environnement d'une application, demander et répondre avant et/ou après le que l'application Slim ne soit appelée.

### Architecture des Middlewares 

Pensez à une application Slim comme le coeur d'un oignon. Chaque couche de l'oignon est un middleware. Lorsque vous appelez la méthode `run()` d'une application Slim, la couche la plus externe (le middleware) est appelée en premier. Lorsque vous êtes prêt, ce middleware est responsable de l'invocation éventuellement le middleware suivant. Ce processus va de plus en plus profond dans l'oignon - à travers chaque couche de middleware - jusqu'à ce que le noyau de l'application Slim soit appelée. Ce processus étagé est possible parce que chaque couche de middleware, et l'application Slim elle-même, implémentent une méthode publique `call()`.
Lorsque vous ajoutez un nouveau middleware pour une application Slim, le middleware ajouté deviendra une nouvelle couche extérieure et va entourer la couche précédente de middleware (si il y en a une) ou l'application Slim elle-même.

### Reference de l'Application 

Le but de middleware consiste à inspecter, analyser, ou de modifier l'environnement d'application, demander et répondre avant et/ou après que l'application Slim soit invoquée. Il est facile pour chaque middleware d'obtenir des références pour l'application Slim  principale, son environnement, sa demande et sa réponse:

    <?php
    class MyMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            //L'application Slim
            $app = $this->app;

            //L'environnement
            $env = $app->environment;

            //La requête
            $req = $app->request;

            //La réponse
            $res = $app->response;
        }
    }

Les modifications apportées à l'environnement, la demande, et les objets se propagent immédiatement dans l'application et ses autres couches de middleware. C'est possible parce qu'à chaque couche de middleware est donnée une référence de la même application Slim.

### Référence de Middleware suivante 

Chaque couche de middleware est également une référence à la prochaine couche de middleware interne avec `$ this-> next`. Chaque middleware a La responsabilité d'appeler éventuellement le prochain middleware. Cela permettra à l'application Slim de compléter son cycle de vie complet. Si une couche middleware choisit de **ne pas** appeler la prochaine couche de middleware interne, plus aucun middleware interne ne sera lancé et l'application Slim elle-même ne sera pas exécutée, ainsi, la réponse de l'application sera renvoyée au client HTTP telle quelle.

    <?php
    class MyMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            //Optionnellement appeler le middleware suivant
            $this->next->call();
        }
    }
