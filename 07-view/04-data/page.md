---
title: Données de vues
status: live
---

<div class="alert alert-info">
    <strong>Attention!</strong> Vous ne devez assigner vos données directement dans l'objet view que très rarement. Normalement, vous passez vos données à la vue avec la méthode `render()` de l'application Slim, voir <a href="/pages/view-rendering-templates">Générer des rendus</a>. 
</div>

Les méthodes `setData()` et `appendData()` de l'objet view injectent des données dans l'objet view; les données injectées sont disponibles dans les templates. Les données de vues sont stockées à l'intérieur comme un tableau de clé-valeurs.

### Assigner des données

La méthode `setData()` de l'objet view va réécrire en écrasant les anciennes données. Vous pouvez utiliser cette méthode pour assigner une valeur à une variable:

    <?php
    $app->view->setData('color', 'red');

Les données de la vue vont maintenant contenir une clé “color” dont la valeur est “red”. Vous pouvez aussi utiliser la méthode `setData()` pour fournir un tableau de valeurs:

    <?php
    $app->view->setData(array(
        'color' => 'red',
        'size' => 'medium'
    ));

Souvenez-vous, la méthode `setData()` remplacera toutes les données précédentes.

### Apprendre des données

L'objet view dispose aussi d'une méthode `appendData()` qui apprend les données à la vue (en plus de celles déjà existantes). Cette méthode ne prend qu'un tableau comme argument:

    <?php
    $app->view->appendData(array(
        'foo' => 'bar'
    ));
