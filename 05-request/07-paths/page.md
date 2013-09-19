---
title: Chemins de requête
status: live
---

Chaque requête HTTP reçue par l'application Slim aura une racine URI (root URI) et une ressource URI  (Resource URI)

### Racine URI

La **racine URI** est le chemin URL physique jusqu'au directoire dans lequel l'application Slim est instanciée et tourne. Si une application Slim est instanciée dans **index.php** au sein du répertoire de tête de l'hôte virtuel (document root), la racine URI sera une chaîne de caractères vide. Si l'application Slim est instanciée et tourne dans **index.php**, au sein d'un sous-répertoire physique de la machine, la racine URI sera le chemin jusqu'à ce sous-répertoire avec un slash au début et sans slash de fin.

### Ressource URI

La **ressource URI** est le chemin virtuel d'URI jusqu'à une ressource de l'application. La ressource URI sera comparée aux routes de l'application Slim.

En considérant que l'application Slim est installée dans un sous-répertoire physique **/foo** dans votre document root.
En considérant aussi que l'URL de la requête HTTP (dans la barre de navigation du navigateur) est **/foo/books/1**. La racine URI est **/foo** (chemin jusqu'au répertoire physique où se trouve Slim), et la ressource URI est 
Also assume the full HTTP request URL (what you’d see in the browser location bar) is . The root URI **/books/1**, chemin jusqu'à la ressource de l'application.

Vous pouvez récupérer les racine et ressource URI de la requête HTTP avec les méthodes `getRootUri()` et `getResourceUri()` de l'objet request:

    <?php
    $app = new \Slim\Slim();

    // Récupère l'objet request 
    $req = $app->request;

    // Récupère la racine URI
    $rootUri = $req->getRootUri();

    // Récupère la ressource URI
    $resourceUri = $req->getResourceUri();
