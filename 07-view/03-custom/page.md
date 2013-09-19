---
title: Vues personnalisées
status: live
---

Une application Slim délègue le rendu de ses modèles à son objet view. Une vue personnalisée est une classe fille de `\Slim\View` qui implémente l'interface:

    <?php
    public render(string $template);

La méthode `render` de l'objet view doit retourner le contenu généré dans le template spécifié par son paramètre `$template`. Quand la méthode `render` d'un objet view parsonnalisé est appelée, le chemin du template (relatif au paramètre “templates.path” de l'application Slim) est passé comme son argument. Voici un exemple de vue personnalisée (ou d'objet view personnalisé):

    <?php
    class CustomView extends \Slim\View
    {
        public function render($template)
        {
            return 'Le rendu final généré';
        }
    }

La vue personnalisée peut faire ce qu'elle veut tant qu'elle renvoie le rendu comme une chaîne de caractères. 
Une vue personnalisée rend facile d'intégrer un système de template PHP comme Twig ou Smarty.

<div class="alert alert-info">
    <strong>Attention!</strong> Une vue personnalisée peut accéder à des données qui lui sont passées par <code>render()</code> via <code>$this->data</code>.
</div>

Vous pouvez parcourir des vues personnalisées prêtes à l'emploi qui fonctionnent avec des moteurs de template PHP dans le répertoire Slim-Extras sur GitHub.

### Exemple de vue

    <?php
    class CustomView extends \Slim\View
    {
        public function render($template)
        {
            // $template === 'show.php'
            // $this->data['title'] === 'Sahara'
        }
    }

### Exemple d'intégration

Si la vue personnalisée n'est pas trouvée par un autoloader enregistré, elle doit être requise avant que l'application Slim soit instanciée.

    <?php
    require 'CustomView.php';

    $app = new \Slim\Slim(array(
        'view' => new CustomView()
    ));

    $app->get('/books/:id', function ($id) use ($app) {
        $app->render('show.php', array('title' => 'Sahara'));
    });

    $app->run();
