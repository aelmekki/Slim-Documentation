---
title: Généralités sur le cache HTTP
status: live
---

Une application Slim fournit un support pour la gestion du cache HTTP avec ses méthodes d'aide `etag()`, `lastModified()` et `expires()`.
Le mieux c'est d'utiliser `etag()` ou `lastModified()` - en couple avec `expires()` - par route;
n'utilisez jamais `etag()` et `lastModified()` ensemble dans la même fonction de rappel pour une route.

Les méthodes `etag()` et `lastModified()` doivent être appelées dans une fonction de rappel de route avant le reste du code; cela permet à Slim de vérifier les requêtes GET avant d'appeler le reste du code.

Que ce soit `etag()` ou `lastModified()`, elles demandent au client HTTP de garder en mémoire les ressources de réponse dans le cache client.
La méthode `expires()` indique au client HTTP quand son cache (celui du client) doit être considéré comme dépassé.
