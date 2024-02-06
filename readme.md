<img src="https://uploads-ssl.webflow.com/6108e07db6795265f203a636/61f90cbb8c06383f8944720e_ML%20Flow.png" width="600px" style="padding-bottom: 12px;">

# Lancer un serveur MLflow dans un conteneur Docker

Vous trouverez dans ce dépôt, tous les éléments nécessaires pour démarrer **un [serveur MLflow](https://mlflow.org/docs/latest/tracking/tutorials/remote-server.html) dans un conteneur Docker**. Vous pouvez lancer ce conteneur : 
- **en local sur votre machine**,
- **à distance depuis un [codespace](https://docs.github.com/fr/codespaces/overview) GitHub** (un serveur distant accessible depuis un notebook Google Colab). En lançant ce conteneur depuis un codespace, vous pouvez tracker vos expérience de machine learning depuis un **Google Colab**.

## TODO

- Docker Compose : changer le nom par défaut de l'image construite avec le Dockerfile (et du container)
- Merger tutorial.ipynb, train.py et try-model.py dans un Colab (https://drive.google.com/file/d/1kfeJkVBVEAmaY1-84BOylGPZnDAV6C-v/view?usp=sharing)
- Ajouter une base de donnée Postegresql
- Ajouter un "artefact store"
- Où stocker les variables d'environnement pour Artefact store et Database ?

## A propos de MLflow

[MLflow](https://mlflow.org/docs/latest/introduction/index.html) fournit une suite d'outils visant à simplifier le flux de travail ML. Il est conçu pour aider les développeurs tout au long des différentes étapes de développement et de déploiement du ML. Les fonctionnalités principales de MLflow  sont :

- **Tracking**: MLflow Tracking fournit à la fois une API et une interface utilisateur dédiées à la journalisation des paramètres, des versions de code, des métriques et des artefacts pendant le processus ML.
- **Model Registry**: Une approche systématique de la gestion des modèles, aidant à gérer différentes versions de modèles et assurant une production fluide.
- **MLflow Deployments for LLMs**: Un serveur équipé d'API standardisées pour un accès simplifié aux modèles SaaS et OSS LLM.
- **Evaluate**: Outils conçus pour une analyse et une comparaison approfondies des modèles.
- **Prompt Engineering UI**: Outils conçus pour une analyse et une comparaison approfondies des modèles.
- **Recipes**: Lignes directrices pour structurer les projets ML, visant à garantir des résultats optimisés pour des scénarios de déploiement réels.
- **Projects**: Standardisez l'empaquetage du code ML, des flux de travail et des artefacts, en définissant les dépendances et les méthodes d'exécution pour chaque projet.


## Installation

### Créer un serveur local

1. Cloner ce dépôt `git clone https://github.com/DavidScanu/mlflow-server.git`
2. Se déplacer à l'intérieur du dépôt GitHub : `cd mlflow-server/`
3. Lancer le conteneur du serveur MLflow : `docker compose up -d`
4. Accéder à l'interface utilisateur en accédant à `http://127.0.0.1:5001` ou `http://localhost:5001` dans votre navigateur.

### Créer un serveur dans codespace (remote server) 

1. Créer un codespace à partir de ce dépôt (UI de GitHub: Code / Codespaces / +)
2. Installer les bibliothèques python : `pip install mlflow psycopg2-binary boto3`
3. Lancer le conteneur du serveur MLflow : `docker compose up -d` (à enlever)
4. Accéder à l'interface utilisateur en accédant à l'URL public exposée par codespace. Dans le Terminal, cliquer sur "Ports", puis définir l'URL du port 5001 comme public.


## Démonstration

Pour tester le serveur MLflow : 

1. Créer un environnement python : `python3 -m venv .venv`
2. Activer l'environnement python : `source .venv/bin/activate`
3. Installer les bibliothèques python : `pip install mlflow psycopg2-binary boto3 scikit-learn==1.2.2`
4. Entrainer un modèle : `python3 demo/train.py`. Vous devez voir apparaître un nouveau run dans l'UI MLflow.
5. Utiliser un modèle : `python3 demo/try-model.py`. Cette commande retourne un modèle dans le Terminal. 

## Guide d'utilisation

### Utiliser le serveur MLflow depuis votre environnement local

Pour utiliser le serveur MLflow comme **serveur local** (c-à-d dans le codespace lui-même), utiliser l'une de ces deux méthodes :

- Dans votre code Python : `mlflow.set_tracking_uri("http://127.0.0.1:5001")` ou `mlflow.set_tracking_uri("http://localhost:5001")`
- Avec une variable d'environnement : `export MLFLOW_TRACKING_URI=http://127.0.0.1:5001` ou `export MLFLOW_TRACKING_URI=http://localhost:5001`

### Utiliser le serveur depuis votre environnement distant

Pour utiliser le serveur MLflow comme **serveur distant** (exemple depuis: Colab, VM ou depuis votre PC), il faut définir l'**URI de tracking MLflow** en utilisant l'une de ces deux méthodes :

- Dans votre code Python : `mlflow.set_tracking_uri("http://url-public-exposee-par-codespace-github")`
- Avec une variable d'environnement  : `export MLFLOW_TRACKING_URI=http://url-public-exposee-par-codespace-github`

Voici un exemple : 

- Copier ce notebook Colab [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://drive.google.com/file/d/1kfeJkVBVEAmaY1-84BOylGPZnDAV6C-v/view?usp=sharing)
- Changer la variable `mlflow_tracking_uri`
- Changer la variable `run_id`


## A Propos

**David Scanu**, étudiant en Intelligence artificielle à l'école **Microsoft IA par Simplon et ISEN**.

<a href="https://www.linkedin.com/in/davidscanu14/"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" ></a>
