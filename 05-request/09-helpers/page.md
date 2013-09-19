---
title: Outlis de requête
status: live
---

L'objet request de l'application Slim fourni une liste de méthodes d'aide pour récupérer des informations courantes dans les requêtes HTTP:

### Type de contenu

Récupérez le type de contenu de la requête (par exemple "application/json;charset=utf-8"):

    <?php
    $req = $app->request;
    $req->getContentType();

### Type de media

Récupérez le type de média de la requête (par exemple "application/json"):

    <?php
    $req = $app->request;
    $req->getMediaType();

### Paramètres du type de média

Récupérez les paramètres du type de média de la requête (par exemple [charset => "utf-8"]):

    <?php
    $req = $app->request;
    $req->getMediaTypeParams();

### Charset de contenu

Récupérez le charset de contenu (par exemple "utf-8"):

    <?php
    $req = $app->request;
    $req->getContentCharset();

### Taille du contenu

Récupérez la taille du contenu

    <?php
    $req = $app->request;
    $req->getContentLength();

### L'hôte

Récupérez l'hôte de la requête (par exemple "slimframework.com"):

    <?php
    $req = $app->request;
    $req->getHost();

### Host with Port

Récupérez l'hôte de la requête avec le port (par exemple "slimframework.com:80"):

    <?php
    $req = $app->request;
    $req->getHostWithPort();

### Port

Récupérez le port de la requête (par exemple 80):

    <?php
    $req = $app->request;
    $req->getPort();

### Schéma

Récupérez le schéma de la requête (par exemple "http" ou "https"):

    <?php
    $req = $app->request;
    $req->getScheme();

### Chemin

Récupérez le chemin de la requête (root URI + resource URI):

    <?php
    $req = $app->request;
    $req->getPath();

### URL

Récupérez l'URL de la requête (scheme + host [ + port si non standard ]):

    <?php
    $req = $app->request;
    $req->getUrl();

### Adresse IP 

Récupérez l'adresse IP de la requête:

    <?php
    $req = $app->request;
    $req->getIp();

### Référant

Récupérez le référant de la requête:

    <?php
    $req = $app->request;
    $req->getReferrer();

### User Agent

Récupérez le user agent de la requête:

    <?php
    $req = $app->request;
    $req->getUserAgent();
