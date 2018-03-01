[![Python](https://img.shields.io/badge/python-3.6-blue.svg)](https://docs.python.org/3/)
[![Sphinx](https://img.shields.io/badge/sphinx-1.7-blue.svg)](https://www.djangoproject.com)
[![Documentation Status](https://readthedocs.org/projects/oser-tech-docs/badge/?version=latest)](http://oser-tech-docs.readthedocs.io/fr/latest/?badge=latest)

# Documentation technique du site web d'OSER

Ce dépôt contient le code de la documentation hébergée sur [ReadTheDocs](http://oser-tech-docs.readthedocs.io/fr/latest/). Tu as envie de participer à la documentation ? Suis le guide !

## Dépendances

La documentation est générée à l'aide de [Sphinx](http://www.sphinx-doc.org/en/master/), un outil de documentation intelligente écrit en Python. Il n'y a pas de dépendances particulières hormis Python 3+.

## Installation

Vous pouvez installez `oser-tech-docs` dans un environnement virtuel, ou _virtualenv_ (recommandé), ou bien sur la distribution Python de votre système.

Procédure d'installation :

1. Clônez le dépôt : `$ git clone`
2. Rendez-vous dans le dossier du dépôt `$ cd oser-tech-docs/`
3. Installez les dépendances Python avec `pip`\* : `$ pip install -r requirements.txt`
4. Rendez-vous dans le dossier source de la documentation : `$ cd doc/s` ;
4. Lancez le serveur HTML `$ make livehtml`

La documentation devrait alors être disponible à l'adresse [`http://127.0.0.1:8000`](http://127.0.0.1:8000) (précisée dans l'affichage de `$ make livehtml`). Le serveur a une fonctionnalité *hot reload* : à chaque changement dans les fichiers sources, celui-ci regénère le HTML et actualise le navigateur. Pratique !

\* Si vous utilisez un virtualenv, pensez à le créer et à l'activer avant cette étape. Appelez-le `env` afin qu'il soit ignoré par Git. Sur macOS, utilisez `pip3` (au lieu de `pip`) si vous n'êtes pas dans un virtualenv pour installer les dépendances dans Python 3 et non le Python 2 du système.
