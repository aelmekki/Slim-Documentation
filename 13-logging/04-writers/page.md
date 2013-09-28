---
title: Log Writers
status: live
---

L'objet log d'une application Slim a un log writer. Le log writer is responsable de l'envoi des messages loggués dans la sortie de l'application (par exemple: STDERR, un fichier de log, un web service, Twitter, ou une base de données). De base, l'objet log d'une application Slim à un log writer de classe `\Slim\LogFileWriter`; Ce log writer écrit directement dans la ressource fournise par la clé de l'environnement d'application **slim.errors** (par  défaut, c'est “php://stderr”). Vous pouvez aussi définir un log writer personnalisé.

### Comment utiliser un log writer personnalisé

Un log writer personnalisé doit implémenter l'interface suivante:

    <?php
    public function write(mixed $message);

Vous devez indiquer à l'objet log de l'application Slim d'utiliser votre log writer personnalisé. Vous pouvez le faire à l'instanciation comme celas:

    <?php
    $app = new \Slim\Slim(array(
        'log.writer' => new MyLogWriter()
    ));

Vous pouvez aussi en définir un avec un middleware comme cela:

    <?php
    class CustomLogWriterMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            //Définit le nouveau log writer
            $$this->app->log->setWriter(new \MyLogWriter());

            //Appeler le middleware suivant
            $this->next->call();
        }
    }

Vous pouvez aussi le faire dans une fonction de rappel ou un hook, comme cela:

    <?php
    $app->hook('slim.before', function () use ($app) {
        $app->log->setWriter(new \MyLogWriter());
    });

Si vous avez seulement besoin de rediriger la sortie d'erreur à une ressource différente, utilisez le log writer par défaut le Slim application. Tout ce que vous avez à faire, c'est définir la variable d'environnement **slim.errors** à une ressource valide.
