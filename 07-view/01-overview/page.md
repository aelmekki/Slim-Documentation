---
title: Généralités des vues
status: live
---

Une application Slim délègue le rendu de ses templates à son objet view. Une view est une classe fille de `\Slim\View` qui implémente cette interface:

    <?php
    public render(string $template);

La méthode `render()` de l'objet view doit retourner le contenu rendu du modèle spécifié par l'argument `$template`.
