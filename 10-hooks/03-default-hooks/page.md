---
title: Crochets par défaut
status: live
---

Voici les crochets par défaut qui sont toujours appelés dans une application Slim:

slim.before
: Ce crochet est appelé avant que l'application Slim soit exécutée et avant que la mise en mémoire tampon de sortie ne soit activée. Ce crochet n'est appelé qu'une fois au cours du cycle de vie d'une application Slim.

slim.before.router
: Ce crochet est invoqué une fois que la mise en mémoire tampon de sortie est activée et avant que le routeur ne soit actif. Ce crochet n'est appelé qu'une fois au cours du cycle de vie d'une application Slim.

slim.before.dispatch
: Ce crochet est appelé avant qu'une route ne soit appelée. Habituellement, ce crochet n'est appelé qu'une fois au cours du cycle de vie d'une application Slim, mais il peut être invoqué plusieurs fois si une route choisit de passer à une route subséquente.

slim.after.dispatch
: Ce crochet est appelé après qu'une route ait été  appelée. Habituellement, ce crochet n'est appelé qu'une fois au cours du cycle de vie d'une application Slim, mais il peut être invoqué plusieurs fois si une route choisit de passer à une route subséquente.

slim.after.router
: Ce crochet est appelé une fois que le routeur a dispatché la requête, avant que la réponse ne soit envoyée au client et après que la sortie tampon ne soit arrêtée. Il est appelé une seule fois dans le cycle de vie d'une application Slim.

slim.after
: Ce crochet est appelé une fois que la réponse est envoyée au client et après que la sortie tampon ait été arrêtée. Il est appelé une seule fois dans le cycle de vie d'une application Slim.
