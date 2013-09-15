---
title: Généralités sur le routage
status: live
---

The Slim Framework vous aide à mapper vos URIs aux fonctions de rappel pour des méthodes de requête HTTP spécifiques (par exemple GET, POST, PUT, DELETE, OPTIONS ou HEAD). Une application Slim va appeler la première route qui correspond à la requête HTTP de l'URI ainsi qu'à la méthode utilisée.

Si l'application Slim ne trouve pas de route qui corresponde à la méthode ainsi que l'URI de la requête HTTP, elle va automatiquement retourner une réponse d'erreur du type **404 Not Found**.
