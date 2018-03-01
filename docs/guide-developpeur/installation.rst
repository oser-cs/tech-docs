============
Installation
============

Le site d'OSER est décomposée en deux parties : le backend et le frontend qui communiquent essentiellement via une API REST. En conséquence, il y a **deux serveurs de développement** à installer : le serveur backend et le serveur frontend.

Cette page vous indique étape par étape comment installer chacun de ces serveurs en local. Cela vous permet de faire tourner le site sur votre propre ordinateur afin d'y apporter des modifications.

Prérequis
=========

Git
---

Vous aurez besoin de `Git <https://git-scm.com>`_ pour cloner le dépôt. Une connaissance basique de ce système de gestion de version est requise. Référez-vous à des tutoriels (par exemple `celui-ci <https://try.github.io/levels/1/challenges/1>`_) si besoin. :)

Backend
-------

Python et virtualenv
********************

Le backend du site repose sur Django et donc Python. Munissez-vous de `Python 3.5+ <https://www.python.org/downloads/>`_ et de `virtualenv <https://pypi.python.org/pypi/virtualenv>`_ si ce n'est pas encore fait. Vous pouvez aussi consulter la page :doc:`ressources-apprentissage/dev-python` pour plus d'informations sur l'installation et l'utilisation de ``virtualenv``.

Django et le Django REST Framework
**********************************

Une connaissance minimale de Django est requise, c'est pourquoi je vous recommande fortement de suivre quelques tutoriels, par exemple `celui d'OpenClassrooms <https://openclassrooms.com/courses/introduction-au-framework-django>`_. Vous pouvez passer rapidement sur les templates, car comme précisé en introduction cette partie de Django n'est pas utilisée ici.

Enfin, la gestion de l'API REST suppose une connaissance minimale du `Django REST Framework (DRF) <http://www.django-rest-framework.org>`_, une surcouche de Django qui permet d'écrire facilement et efficacement une API REST. Jetez un œil à la page `Tutorials and resources <http://www.django-rest-framework.org/topics/tutorials-and-resources/>`_ du DRF pour bien démarrer.

Frontend
--------

.. note:: En construction

Serveur backend
================

Nous allons voir ici comment installer l'environnement de développement backend du site. Le backend concerne, rappelons-le, tout ce qui ne concerne pas l'interface utilisateur : bases de données, tâches de fond, services… À la fin de ce processus, vous aurez un serveur backend local fonctionnel !

Installation des dépendances
----------------------------

Tout d'abord, clonez le dépôt du backend sur votre ordinateur :
::
  $ git clone https://github.com/oser-cs/oser-backend.git
  $ cd oser-backend

Créez ensuite un environnement virtuel appelé ``env`` puis activez-le :
::
  oser-backend $ virtualenv env
  oser-backend $ source env/bin/activate

Installez les dépendances Python du back en utilisant ``pip`` :
::
  (env) oser-backend $ pip install -r requirements.txt

Vous pouvez ensuite vous placer dans le dossier source, d'où vous effectuerez la majorité de votre travail :
::
  (env) oser-backend $ cd oser_backend

.. note:: Les aperçus shell ci-après ne feront plus apparaître le préfixe de la ligne de commande. Sauf indication contraire, on supposera que le dossier courant est ``oser-backend/oser_backend`` (là où se situe le fichier ``manage.py``) et que l'environnement virtuel est, le cas échéant, activé.

Configuration de la base de données
-----------------------------------

Pour tourner, le back a besoin d'une **base de données**. À ce stade, vous n'en avez pas encore. Django permet de générer la base de données et son schéma grâce aux **migrations** : il analyse la base de données actuelle et détermine automatiquement les opérations à effectuer pour la rendre opérationnelle et synchronisée avec le code source.

Du coup, creéz puis exécutez les migrations Django :
::
  $ python manage.py makemigrations
  $ python manage.py migrate

Exécution des tests
-------------------

Le serveur backend dispose d'une batterie de tests qui permettent de s'assurer que la majorité des fonctionnalités est opérationnelle. Lancez les tests pour vous assurer que tout fonctionne comme prévu :
::
  $ python manage.py test

Population de la base de données (optionnel)
--------------------------------------------

Vous pouvez peupler la base de données avec des données factices. Cette étape est recommandée si vous prévoyez d'accéder au frontend (sinon, le site aura l'air bien vide…).

Pour cela, utilisez la commande ``populatedb`` :
::
  $ python manage.py populatedb

.. todo::
  Guide d'utilisation et de maintenance de ``populatedb``.

Démarrage du site en mode développement
---------------------------------------

Une fois tout ceci fait, vous pouvez démarrer le serveur local Django avec la commande ``runserver`` :
::
  (env) oser_backend $ python manage.py runserver

Si vous vous rendez à l'adresse `http://localhost:8000/ <http://localhost:8000/>`_, vous devriez voir apparaître la documentation de l'API. Si c'est le cas, le serveur Django est fonctionnel ! 👍

.. image:: /media/api-docs.png

Détail des dépendances
----------------------

.. _Django : https://www.djangoproject.com
.. _release news: https://www.djangoproject.com/weblog/2017/dec/02/django-20-released/)
.. _Django REST Framework : http://www.django-rest-framework.org
.. _DRY Rest Permissions : https://github.com/dbkaplan/dry-rest-permissions
.. _FactoryBoy : http://factoryboy.readthedocs.io/en/latest/index.html

Django
******

Django_ est un framework de développement web pour Python.

Le site d'OSER utilise Django en version 2.0.

> À l'heure actuelle, peu de tutoriels Django se basent sur la version 2.0, mais il y a en fait très peu de changements non-rétro-compatibles par rapport à la version 1.11, et aucun changement n'est réellement critique. Les améliorations apportées par la version 2.0 sont intéressantes, on peut notamment citer le système d'écriture des URLs qui est grandement simplifié. Pour plus d'infos, lire la `release news`_ associée.

Django REST Framework
*********************

Le `Django REST Framework`_ (DRF) permet d'écrire facilement des API REST avec Django. Le site d'OSER utilise le DRF en version 3.7.3. Cette version est entièrement compatible avec Django 2.0.

DRY Rest Permissions
********************

`DRY REST Permissions`_ est utilisé pour définir les permissions de l'API directement sur les modèles Django.

FactoryBoy
**********

`FactoryBoy`_ est utilisé pour faciliter la création d'objets de test en définissant des usines (*factories*) directement à partir des modèles Django. Les usines sont définies dans ``oser_backend/tests/factory.py``.
