---
title: Généralités
status: live
---

Soyons réaliste, parfois, les choses se passent mal. C'est important d'intercepter les erreurs et de les traiter correctement. Une application Slim fournit une liste de méthodes d'aides pour gérer les erreurs et les exceptions.

### Notes Importantes

* Une application Slim respecte votre paramètre `error_reporting`;
* Une application Slim gère seulement les erreurs et exceptions créées dans l'application;
* Une application Slim transforme les erreurs en objet de type `ErrorException` et les "throw";
* Une application Slim utilise son propre gestionnaire d'erreurs si le paramètre `debug` vaut "true"; sinon, il utilise un gestionnaire personnalisé.
