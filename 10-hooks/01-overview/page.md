---
title: Généralités sur les crochets
status: live
---

Une application Slim fournit une liste de crochets auxquels vous pouvez abonner vos propres fonctions de rappel.

### Qu'est-ce qu'un crochet?

Un “crochet” est un moment du cycle de vie d'une application Slim où une liste prioritaire de fonctions appelables qui lui sont liées (au crochet) sera invoquée. Un crochet est identifié par une chaîne de caractères.

Par “fonction appelable” j'entends n'importe quel objet qui returne `true` à la fonction `is_callable()`. 
Une fonction appelable est liée à un crochet et est appelée quand le crochet est appelé. Si plusieurs fonctions sont liées à un même crochet, chaque fonction est appelée dans l'ordre de leur priorités et dans lequel elles ont été ajoutées.
