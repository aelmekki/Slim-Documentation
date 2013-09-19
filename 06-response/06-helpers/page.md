---
title: Aides
status: live
---

L'objet response fourni des méthodes d'aide pour inspecter et interagir avec la réponse HTTP.

### Finalize

La méthode `finalize()` de l'objet response retourne un tableau `[statut, en-tête, corps]`. Le statut est un entier; le header est une structure de données itérables; et le corps une chaîne de caractères. Que vous créiez un nouvel objet `\Slim\Http\Response` dans l'application Slim ou un middleware, vous devez appeler la méthode `finalize()` pour produire le statut, l'en-tête et le corps de la réponse HTTP.

    <?php
    /**
     * Préparer un nouvel objet response
     */
    $res = new \Slim\Http\Response();
    $res->setStatus(400);
    $res->write('Vous avez fait une mauvaise requête');
    $res->headers->set('Content-Type', 'text/plain');

    /**
     * Finalize
     * @return [
     *     200,
     *     ['Content-type' => 'text/plain'],
     *     'Vous avez fait une mauvaise requête'
     * ]
     */
    $array = $res->finalize();

### Redirection

La méthode `redirect()` de l'objet response va assigner le statut et l'en-tête  **Location:** nécessaires pour renvoyer une réponse **3xx Redirect**.

    <?php
    $app->response->redirect('/foo', 303);

### Introspection de statut

L'objet response fourni d'autres méthodes d'aide pour inspecter son statut courant. Toutes les méthodes qui suivent renvoient un booléen:

    <?php
    $res = $app->response;

    // Est-ce une réponse informelle?
    $res->isInformational();

    // Est-ce une réponse 200?
    $res->isOk();

    // Est-ce une réponse de type 2XX?
    $res->isSuccessful();

    // Est-ce une réponse de type 3XX?
    $res->isRedirection();

    // Est-ce une réponse de redirection spécifique? (301, 302, 303, 307)
    $res->isRedirect();

    // Est-ce une réponse interdite?
    $res->isForbidden();

    // Est-ce une réponse de type non-trouvé?
    $res->isNotFound();

    // Est-ce une erreur de réponse du client?
    $res->isClientError();

    // Est-ce une erreur de réponse du serveur?
    $res->isServerError();
