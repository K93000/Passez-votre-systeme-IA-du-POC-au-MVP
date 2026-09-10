#  Passage du POC au MVP — Puls-Events

[![AWS](https://img.shields.io/badge/AWS-ECS%20Fargate%20%7C%20Redis%20%7C%20CloudWatch-232F3E?logo=amazon-aws&logoColor=white)](#)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](#)
[![Qdrant](https://img.shields.io/badge/Qdrant-Vector%20Database-DC2626)](#)
[![Mistral AI](https://img.shields.io/badge/Mistral_AI-LLM%20%26%20Embeddings-FF7000)](#)

##  Présentation du projet

Ce projet consiste à faire évoluer un prototype de chatbot événementiel vers une architecture MVP plus robuste, évolutive et adaptée à une utilisation en production.

L’objectif est de permettre aux utilisateurs de rechercher des événements culturels en langage naturel, en tenant compte de leur localisation, de leurs préférences et du contexte de la conversation.

---

##  Contexte et objectifs du MVP

Le projet part d’un prototype de chatbot spécialisé dans la recherche d’événements culturels, qui a permis de valider l’intérêt de la recherche en langage naturel.

La mission consiste à transformer ce prototype en MVP pour :

- conserver le contexte des échanges avec l’utilisateur ;
- améliorer la recherche par ville et localisation géographique ;
- actualiser régulièrement les événements depuis le flux OpenAgenda ;
- compléter les résultats avec une recherche Web si nécessaire ;
- suivre les performances et traiter les erreurs ;
- disposer d’une architecture Cloud évolutive reposant sur des services managés.

---

##  Architecture cible

L’architecture proposée repose sur :

- **AWS ECS Fargate** pour héberger l’API FastAPI ;
- **Amazon API Gateway** pour exposer et sécuriser l’API ;
- **Qdrant Cloud** pour la recherche vectorielle et les filtres géographiques ;
- **Amazon ElastiCache for Redis** pour la mémoire conversationnelle ;
- **Mistral AI** pour les embeddings et la génération de réponses ;
- **smolagents** pour l’orchestration des outils et de la recherche Web ;
- **OpenAgenda** pour l’alimentation en événements ;
- **Amazon CloudWatch et LangSmith** pour l’observabilité.

---

##  Documents du projet

| Livrable | Format | Lien |
| :--- | :---: | :--- |
| **Rapport de gestion de projet** | PDF | [Consulter le rapport](./Rapport%20de%20gestion%20de%20projet.pdf) |
| **Support de présentation** | PPTX | [Consulter la présentation](./Presentation.pptx) |

---

##  Travaux réalisés

Dans le cadre de cette mission, j’ai réalisé :

- l’analyse du prototype existant et l’identification de ses limites ;
- le cadrage fonctionnel du MVP et l’étude des solutions Cloud ;
- la conception de l’architecture cible et le découplage des composants ;
- la définition du backlog fonctionnel avec la méthode MoSCoW ;
- l’estimation de la charge de développement ;
- l’estimation des coûts de construction et d’exploitation ;
- la proposition d’un planning de réalisation sur 10 semaines.

---

##  Technologies étudiées et retenues

`Python` • `FastAPI` • `AWS ECS Fargate` • `Amazon API Gateway` • `Amazon ElastiCache for Redis` • `Qdrant Cloud` • `Mistral AI` • `smolagents` • `OpenAgenda` • `LangSmith` • `Amazon CloudWatch`

---

##  Portfolio et compétences mobilisées

###  Compétences démontrées

- analyse et cadrage d’un besoin métier ;
- conception d’une architecture IA et Cloud ;
- étude et sélection de solutions techniques ;
- conception d’un système RAG évolutif et géolocalisé ;
- conception d’une mémoire conversationnelle ;
- estimation des coûts Cloud ;
- planification de projet ;
- documentation technique ;
- présentation et vulgarisation de choix techniques.

###  À propos

Projet réalisé dans le cadre de ma formation Data Engineer OpenClassrooms.

Ce projet porte sur la conception du passage d’un prototype IA à un MVP Cloud évolutif pour la plateforme Puls-Events.
