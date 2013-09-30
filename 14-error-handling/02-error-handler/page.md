---
title: Gestionnaire d'erreur
status: live
---

Vous pouvez utiliser la méthode `error()` de Slim pour créer un gestionnaire d'erreurs personnalisé à appeler quand une erreur ou une exception apparaît. Les gestionnaires d'erreurs personnalisés sont seulement appelés si le débogage de l'application est désactivé.

Un gestionnaire d'erreurs personnalisé doit fournir un message facile à comprendre pour l'utilisateur. Tout comme la méthode `notFound()` de Slim, la méthode `error()` agit comme un getter et un setter.

### Définir un gestionnaire d'erreurs personnalisé

Vous pouvez définir un gestionnaire d'erreur personnalisé en passant une fonction dans la méthode `error()` de Slim comme argument.

    <?php
    $app = new \Slim\Slim();
    $app->error(function (\Exception $e) use ($app) {
        $app->render('error.php');
    });

Dans cet exemple, le gestionnaire d'erreurs personnalisé prend une Exception comme argument. Cela vous permet de répondre différemment en fonction des différentes exceptions.

### Appeler un gestionnaire d'erreurs personnalisé

Normalement, l'application Slim va automatiquement appeler le gestionnaire d'erreurs quand une erreur ou une exception se produit. Malgré cela, vous pouvez aussi l'appeler manuellement avec la méthode `error()` sans argument.
