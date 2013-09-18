---
title: Généralités sur l'Environnement
status: live
---

The Slim Framework implémente un dérivé du [protocole Rack](http://rack.rubyforge.org/doc/files/SPEC.html). Quand vous instanciez une application Slim, cela va immédiatement inspecter la variable globale `$_SERVER` et créer une liste de variables d'environnement qui dictent la conduite de l'application.

### Qu'est-ce que l'Environnement?

L'environnement d'une application Slim est un tableau associatif de paramètres qui sont passés une fois et accessibles à l'application Slim et son middleware. Vous êtes libres de modifier les variables d'environnement pendant l'exécution; les changements se propageront immédiatement dans l'application.

Quand vous instanciez une application Slim, les variables d'environnement sont dérivées de la super variable `$_SERVER`; Vous ne devez pas l'attribuer vous-même. Quoi qu'il en soit, vous êtes libres de modifier ou surcharger ces variables dans Slim.

Ces variables sont fondamentales pour déterminer comment votre application tourne: les ressources URI, la méthode HTTP, le corps d'une requête HTTP, les paramètres d'une requête URL, les erreurs et bien plus encore. Le middleware, décrit plus tard, vous donne le pouvoir de manipuler les variables d'environnement avant et/ou après que l'application Slim soit lancée.

### Variables d'Environnement

Le texte suivant est un extrait des informations disponibles sur <http://rack.rubyforge.org/doc/files/SPEC.html>. Le tableau d'environnement doit inclure ces variables:

REQUEST_METHOD
: La méthode de requête HTTP. C'est requis même si c'est une chaîne de caractères vide.

SCRIPT_NAME
: La première partie d'une requete URI correspond au répertoire physique dans lequel votre application Slim est installée - de sorte que l'application connaisse sa localisation virtuelle. Cela peut-être une chaîne vide si l'application est installée au "top-niveau" de la racine. Ce ne sera jamais un slash.

PATH_INFO
: La partie restante du de la requête URI, qui détermine l'emplacement virtuel de la ressource cible de la requête HTTP dans le cadre de l'application Slim. Il y aura toujours un slash qu peut être seul ou non.

QUERY_STRING
: La partie de l'URI de la requête HTTP après (mais sans inclure) le "?". C'est requis mais peut être une chaîne vide.

SERVER_NAME
: Quand elle est combinée avec `SCRIPT_NAME` et `PATH_INFO`, elle peut être utilisée pour créer des URL complète à une ressource de l'application. En revanche, si `HTTP_HOST` existe, elle doit être utilisée à la place. C'est requis et ne doit jamais être une chaîne de caractères vide.

SERVER_PORT
: Quand elle est combinée avec `SCRIPT_NAME` et `PATH_INFO`, elle peut être utilisée pour créer des URL complète à une ressource de l'application. C'est requis et ne doit jamais être une chaîne de caractères vide.

HTTP_*
: Variables qui correspondent aux en-têtes envoyées par le client dans sa requête HTTP. L'existence de ces variables correspond à celles envoyées dans la requête HTTP courante.

slim.url_scheme
: Sera soit “http” soit “https”, cela dépend de l'URL de la requête HTTP.

slim.input
: Sera une chaîne de caractères représentant le corps de la requête HTTP. Si le corps est vide (exemple une requête GET), cela sera une chaîne vide.

slim.errors
: Doit toujours être une ressource d'écriture; par défaut, c'est une ressource en écriture seule qui traite avec `php://stderr`.

Une application Slim peut sauvegarder ses propres données dans l'environnement. Les clés du tableau d'environnement doivent contenir au moins un point et doivent être préfixées avec un préfixe unique (exemple, “prefix.foo”). Le préfixe **slim.** est réservé par Slim et ne doit pas être utilisé. L'environnement ne doit pas contenir les clés `HTTP_CONTENT_TYPE` ou `HTTP_CONTENT_LENGTH` (utilisez les versions sans HTTP_). Les clés CGI (nommées avec une période) doivent avoir des valeurs en chaînes de caractères. Voici les restrictions:

* slim.url_scheme doit être soit “http”, soit “https”.
* `slim.input` doit être une chaîne de caractères.
* Il doit y avoir une ressource d'écriture valide dans `slim.errors`.
* `REQUEST_METHOD` doit être un jeton valide.
* `SCRIPT_NAME`, si elle n'est pas vide, doit démarrer avec "/"
* `PATH_INFO`, si elle n'est pas vide, doit démarrer avec "/"
* `CONTENT_LENGTH`, si donné, soit être composé uniquement de chiffres.
* L'une des variables `SCRIPT_NAME` ou `PATH_INFO` soit être utilisée. `PATH_INFO` doit être "/" si `SCRIPT_NAME` est vide. `SCRIPT_NAME` ne doit jamais être "/", mais peut être vide.
