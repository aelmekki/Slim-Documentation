---
title: Crochets personnalisés
status: live
---

Des crochets personnalisés peuvent être créés et appelés dans une application Slim. Quand un crochet personnalisé est appelé avec `applyHook()`, il invoquera toutes les fonctions qui lui sont liées. C'est exactement pareil pour les crochets de base de Slim. Dans cet exemple, j'applique un crochet personnalisé appelé “mon.nom.de.crochet”. Toutes les fonctions précédemment liées à ce crochet seront appelées.

    <?php
    $app = new \Slim\Slim();
    $app->applyHook('mon.nom.de.crochet');

Quand vous exécutez le code suivant, chaque fonction précédemment assignée au crochet “mon.nom.de.crochet” sera appelé dans l'ordre de priorité (ascendant).

Vous devez enregistrer les fonctions à un crochet avant de l'appliquer. Pensez de cette façon: quand vous appelez la méthode `applyHook()` de Slim, vous lui demandez d'appeler toutes les fonctions enregistrées pour ce nom de crochet.
