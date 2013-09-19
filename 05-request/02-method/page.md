---
title: Méthodes de la requête
status: live
---

Chaque requête HTTP a une méthode (par exemple GET ou POST). Vous pouvez obtenir la requête HTTP courante via l'objet request de Slim:

    /**
     * Quelle est la méthode de la requête?
     * @return string (e.g. GET, POST, PUT, DELETE)
     */
    $app->request->getMethod();

    /**
     * Est-ce une requête GET?
     * @return bool
     */
    $app->request->isGet();

    /**
     * Est-ce une requête POST?
     * @return bool
     */
    $app->request->isPost();

    /**
     * Est-ce une requête PUT?
     * @return bool
     */
    $app->request->isPut();

    /**
     * Est-ce une requête DELETE?
     * @return bool
     */
    $app->request->isDelete();

    /**
     * Est-ce une requête HEAD?
     * @return bool
     */
    $app->request->isHead();

    /**
     * Est-ce une requête OPTIONS?
     * @return bool
     */
    $app->request->isOptions();

    /**
     * Est-ce une requête PATCH?
     * @return bool
     */
    $app->request->isPatch();

    /**
     * Est-ce une requête XHR/AJAX?
     * @return bool
     */
    $app->request->isAjax();
