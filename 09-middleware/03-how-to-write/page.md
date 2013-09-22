---
title: Comment écrire un Middleware
status: live
---

Un middleware d'application Slim doit hériter de  `\Slim\Middleware` et implémenter une méthode publique `call()`. La méthode `call()` ne prend pas d'argument. Un middleware peut implémenter son propre constructeur, ses propriétés et ses méthodes. Je vous encourage à regarder les middlewares de Slim (par exemplesSlim/Middleware/ContentTypes.php ou encore Slim/Middleware/SessionCookie.php).
`\Slim\Middleware`,
Cet exemple est la plus simple des implémentation d'un middleware de Slim. Il hérite de `\Slim\Middleware`, implémente une méthode publique `call()` et appelle le middleware suivant.

    <?php
    class MyMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            $this->next->call();
        }
    }
