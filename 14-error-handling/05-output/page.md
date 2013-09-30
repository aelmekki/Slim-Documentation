---
title: Redirection de sortie
status: live
---

L'environnement d'une application Slim contiendra toujours une clé **slim.errors** avec une valeur comme ressource (où l'on écrit) pour les messages d'erreurs. L'objet log d'une application Slim écrira les messages dans **slim.errors** chaque fois qu'une Exception est attrapée ou que l'objet log est appelé manuellement.

Si vous voulez rediriger la sortie d'erreur, vous pouvez définir votre propre ressource en modifiant les paramètres d'environnement. Je recommande d'utiliser un middleware pour changer l'environnement:

    <?php
    class CustomErrorMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            // Définir la nouvelle sortie d'erreur
            $env = $this->app->environment;
            $env['slim.errors'] = fopen('/chemain/de/la/sortie', 'w');

            // Appeler le middleware suivant
            $this->next->call();
        }
    }

Souvenez-vous, **slim.errors** ne pointe pas forcément un fichier, il pointe n'importe quelle ressource inscriptible.
