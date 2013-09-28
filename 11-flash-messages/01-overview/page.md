---
title: Généralités sur les messages "flash"
status: live
---

<div class="alert alert-info">
    <strong>Attention!</strong> Les messages "flash" ont besoins des sessions. Si vous n'utilisez pas le middleware  
    <code>\Slim\Middleware\SessionCookie</code>, vous devrez créer une session vous-même avec PHP.
</div>

Slim supporte les messages "flash" tout comme Rails et d'autres frameworks web. Les messages "flash" vous permettent de définir de messages qui persisteront jusqu'à la prochaine requête HTTP, mais pas plus. C'est est utile pour afficher des messages à l'utilisateur après un événement ou quand une erreur se produit.

Comme indiqué ci-dessous, les méthodes `flash()` et `flashNow ()` d'une application Slim acceptent deux arguments: une clé et un message.

La clé peut être ce que vous voulez, elle définit la manière dont le message sera accessible dans les modèles d'affichage. Par exemple, si j'invoque la méthode `flash('foo', 'Le message foo')` avec ces arguments, je peux accéder à ce message dans les modèles de la prochaine requête avec `flash['foo']`.

Les messages "flash" sont conservés avec les sessions, les sessions sont nécessaires pour les messages flash. De plus, Les messages "flash" sont stockés dans `$ _SESSION['slim.flash']`.

