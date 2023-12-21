# HumansBestFriend : Guide de Mise en Route et Documentation Détaillée

## Table des Matières

1. [Introduction](#introduction)
2. [Description du Projet](#description-du-projet)
3. [Architecture de l'Application](#architecture-de-lapplication)
4. [Configuration des Services](#configuration-des-services)
5. [Construction et Vérification des Images Docker](#construction-et-vérification-des-images-docker)
6. [Tagging et Publication des Images Docker](#tagging-et-publication-des-images-docker)
7. [Déploiement de l'Application](#déploiement-de-lapplication)
8. [Vérification et Tests](#vérification-et-tests)
9. [Conclusion](#conclusion)

## Introduction

Ce document fournit un guide détaillé pour la mise en place, le déploiement et la vérification de l'application HumansBestFriend, une application distribuée exécutée dans plusieurs conteneurs Docker.

## Description du Projet

HumansBestFriend est une application web interactive permettant aux utilisateurs de voter entre deux options. Elle utilise une combinaison de technologies, notamment Python, Node.js, et .NET, et s'appuie sur Redis pour la messagerie et Postgres pour la base de données.

## Architecture de l'Application

L'application se compose de plusieurs services :

- **Front-end web** (Python) : Interface utilisateur pour le vote.
- **Redis** : Système de file d'attente pour les votes.
- **Worker .NET** : Traitement des votes et stockage dans Postgres.
- **Application web Node.js** : Affichage des résultats des votes en temps réel.
- **Postgres** : Base de données pour la persistance des votes.

## Configuration des Services

Chaque service de l'application est configuré individuellement dans le `docker-compose.yml` et possède son propre Dockerfile pour la construction de l'image.

## Construction et Vérification des Images Docker

1. **Construction des Images** :
   Utilisez la commande suivante pour construire les images Docker à partir de leurs Dockerfiles respectifs :


docker-compose -f docker-compose.build.yml build

2. **Vérification des Images** :
Après la construction, vérifiez les images avec :


sudo docker images


## Tagging et Publication des Images Docker

1. **Tagging des Images** :
Taguez chaque image construite pour le registre Docker local :
- Exemple : `sudo docker tag <nom_service> localhost:5000/<nom_service>`

2. **Démarrage du Registre Docker** :
Si nécessaire, lancez un registre Docker local :

sudo docker pull registry
sudo docker run -d -p 5000:5000 --restart=always --name registry registry:2


3. **Publication des Images** :
Poussez chaque image taguée vers le registre Docker :


sudo docker push localhost:5000/<nom_service>


## Déploiement de l'Application

Déployez l'application en utilisant :

docker-compose up -d


## Vérification et Tests

- Vérifiez que tous les services sont actifs.
- Testez l'accès aux applications `vote` et `result` sur IP_Vm:5001  IP_Vm:5002
- Assurez-vous que les conteneurs communiquent correctement entre eux.

## Conclusion

Ce guide détaille les étapes nécessaires pour configurer, déployer et vérifier l'application HumansBestFriend dans un environnement Docker. Suivez chaque étape attentivement pour garantir un déploiement réussi.


Khalfoun Rayan
Nabil Hatri

