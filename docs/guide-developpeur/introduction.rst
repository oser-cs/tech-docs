============
Introduction
============

Éléments d'historique
=====================

Septembre 2017
  Reformation du secteur Geek, rassemblement de tuteurs intéressés.

Octobre 2017
  Début du développement du site web d'OSER.

Octobre 2017 - Janvier 2018
  Phase d'étude du besoin et de listing des fonctionnalités. Le résultat est un `Trello Geek <https://trello.com/oser_cs_geek>`_ bien fourni, toujours en évolution !

Mi-janvier 2018
  L'implémentation du site a sérieusement démarré. Les priorités : site vitrine et procédure d'inscription administrative des lycéens.

Mi-février 2018
  Le site vitrine est presque abouti.

Choix techniques
================

Décomposition backend/frontend
------------------------------

Tout site internet repose sur une **stack technique** qui constitue l'ensemble des technos utilisées pour réaliser le site. Avec l'avènement des frameworks Javascript, cette stack est de plus en plus souvent décomposée en 2 aspects :

- D'une part le *frontend* qui gère l'interface utilisateur (le rendu dans le navigateur)
- D'autre part le *backend* qui gère le reste, c'est-à-dire essentiellement la base de données, les services, les tâches de fond, etc.

Cette architecture est historiquement motivée par la démultiplication des supports et des environnements (web, mobile : iOS, Android, Windows Phone, natif…) qui n'influencent que l'interface utilisateur mais pas le modèle de données sous-jacent. Ce dernier a donc été extrait dans un modèle *backend as a service*. Les clients frontend multiples font des appels à un backend unique et donc plus facilement maintenable. Par ailleurs, un frontend dédié permet le plus souvent de réaliser des applications plus interactives.

Le site d'OSER emploie cette décomposition. et dispose donc d'un **frontend Javascript/Angular4** et d'un **backend Python/Django** qui communiquent via une **API REST**.

  *Une API REST ? Qu'est-ce que c'est que ça ?*

Vaste sujet ! En essence, une API REST est **une interface de programmation** qui permet de **récupérer des ressources** d'un serveur de données via de **simples requêtes HTTP**. Les données envoyées ou reçues sont encodées selon le format standard **JSON**.

L'intérêt des API REST est de faciliter **l'interopérabilité** et donc l'utilisation d'un **même serveur de données pour plusieurs clients**. On dispose aujourd'hui d'un backend Django qui sert un client Javascript, mais si OSER envisage un jour de développer une app mobile, celle-ci pourra réutiliser le backend développé pour le site en communiquant sur l'API REST. En résumé, voyez simplement l'API REST comme le langage commun qui permet à un client quelconque de communiquer avec le serveur backend.

Technos employées
-----------------

Django et le Django REST Framework
**********************************

Le choix de **Django** pour le back repose sur l'hypothèse que si des tuteurs connaissent un langage de programmation, il y a de fortes chances que ce soit Python. Parmi les frameworks web Python, Django est probablement le plus complet et le plus mature. Le développement d'API est grandement facilité grâce au Django REST Framework. Enfin, les solutions d'hébergement Python se développent de plus en plus, le déploiement ne devrait donc pas poser trop de problèmes.

**Django**

Django est un framework complet qui permet de réaliser un site internet de bout en bout, de la gestion de la base de données à la génération des réponses HTTP en passant par la génération de contenu HTML. Django est structuré en trois grands concepts selon le modèle MVT : le Modèle (gestion de la BDD), la Vue (extraction et mise en forme de données) et le Template (génération de contenu HTML à partir des données de la Vue).

Cependant, comme on l'a dit, **le backend du site ne gère pas l'interface utilisateur**. En conséquence, **la partie Template est complètement bypassée** (on ne l'utilise pas, mais elle reste fonctionnelle) et remplacée par l'API REST que le frontend peut utiliser pour récupérer des données.


**Django REST Framework (DRF)**

Il s'agit d'une bibliothèque qui repose sur Django et permet de développer une API REST en réutilisant les modèles Django. Cela en fait un outil progressif. Par ailleurs, le DRF offre de nombreux outils très intéressants comme la génération de documentation automatique ou l'API parcourable.

Angular 4
*********

Côté front, **Angular** est également le framework Javascript le plus mature. La version 4 est la version actuelle. Il a aussi l'avantage d'imposer une certaine structure (autour de concepts comme les *NgModules*, les *Components* et autres *Services*…) et donc d'établir des conventions que tout le monde peut suivre. Enfin, il utilise TypeScript, une variante de Javascript qui permet d'écrire du Javascript typé (et facilite grandement la détection de bugs en amont, le déboggage de code Javascript n'étant jamais une partie de plaisir).

Sources de documentation
------------------------

- `Django <https://docs.djangoproject.com/en/2.0/>`_
- `Django REST Framework <http://www.django-rest-framework.org>`_
- `Angular 4 <https://angular.io/docs>`_

------

  *Pourquoi ne pas avoir employé un CMS comme Wordpress ?*

Tout d'abord, personne dans l'équipe ne connaissait Wordpress. Ensuite, dès le départ, nous savions que le site d'OSER allait être très interactif et *data-oriented*. Il nous a semblé qu'opter pour une solution front/back personnalisée, en utilisant des frameworks efficaces, stables et qui ne réinventent pas la roue, permettrait d'obtenir un site adapté aux besoins de l'association.
