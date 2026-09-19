# Passage d'un système IA du POC au MVP — Puls-Events

##  Présentation

Ce projet s'inscrit dans le parcours **Data Engineer d'OpenClassrooms**.

La mission consiste à faire évoluer un système d'IA existant, développé sous forme de **Proof of Concept (POC)**, vers une proposition de **Minimum Viable Product (MVP)** exploitable et évolutive.

Le projet est réalisé dans le contexte de **Puls-Events**, une plateforme permettant de rechercher et découvrir des événements culturels selon différents critères.

L'objectif est de proposer une architecture permettant de rendre le chatbot :

- plus pertinent ;
- capable de prendre en compte le contexte de conversation ;
- capable de mieux gérer la localisation ;
- capable d'utiliser des informations web lorsque nécessaire ;
- observable et monitorable ;
- scalable pour supporter une montée en charge.

---

##  Objectifs du projet

Le projet consiste à :

1. analyser le système POC existant ;
2. identifier ses limites ;
3. analyser les résultats obtenus avec RAGAS ;
4. définir les besoins du futur MVP ;
5. proposer une architecture technique scalable ;
6. sélectionner les technologies adaptées ;
7. construire un backlog priorisé ;
8. établir un planning ;
9. estimer les coûts de développement et d'exploitation ;
10. présenter les choix techniques et financiers.

---

##  Le POC existant

Le POC repose sur une architecture RAG permettant à un utilisateur de poser une question en langage naturel et d'obtenir une réponse générée à partir des données d'événements.

### Technologies du POC

- Python
- LangChain
- Mistral AI
- FAISS
- Streamlit
- OpenAgenda

La base contient environ **3 880 événements culturels** issus d'OpenAgenda.

### Fonctionnement simplifié

```text
Utilisateur
    │
    ▼
Interface Streamlit
    │
    ▼
Question utilisateur
    │
    ▼
Recherche vectorielle FAISS
    │
    ▼
Contexte récupéré
    │
    ▼
Modèle Mistral
    │
    ▼
Réponse
 Évaluation du POC avec RAGAS

Le POC a été évalué avec le framework RAGAS.

Métrique	Résultat
Faithfulness	0,575
Context Precision	0,422
Context Recall	0,233

Le principal point d'attention identifié concerne le Context Recall, qui montre que le système ne récupère pas toujours suffisamment d'informations pertinentes.

Ces résultats servent de base pour définir les améliorations du MVP.

Limites identifiées

L'analyse du POC a permis d'identifier plusieurs limites :

absence de mémoire conversationnelle ;
prise en compte limitée du contexte géographique ;
absence de recherche web dynamique ;
monitoring limité ;
FAISS utilisé localement ;
architecture principalement adaptée à un POC.
 Proposition d'architecture MVP

L'architecture proposée vise à rendre le système plus scalable et plus facilement exploitable.

                         ┌─────────────────┐
                         │    Utilisateur  │
                         └────────┬────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │   API Gateway   │
                         └────────┬────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │ FastAPI /       │
                         │ ECS Fargate     │
                         └───────┬─────────┘
                                 │
              ┌──────────────────┼──────────────────┐
              │                  │                  │
              ▼                  ▼                  ▼
        ┌───────────┐      ┌────────────┐    ┌─────────────┐
        │  Redis    │      │  Qdrant    │    │ smolagents  │
        │  Memory   │      │ Vector DB  │    │ Web Search  │
        └───────────┘      └─────┬──────┘    └─────────────┘
                                 │
                                 ▼
                          ┌─────────────┐
                          │ Mistral AI  │
                          └─────────────┘

              Monitoring :
              CloudWatch + LangSmith
 Technologies proposées
Technologie	Utilisation
AWS	Infrastructure cloud
API Gateway	Point d'entrée de l'application
FastAPI	API backend
ECS Fargate	Exécution des conteneurs
Qdrant Cloud	Base de données vectorielle
Redis / ElastiCache	Mémoire conversationnelle
Mistral AI	Génération des réponses
smolagents	Gestion de la recherche web
OpenAgenda	Source des événements
CloudWatch	Monitoring
LangSmith	Suivi et évaluation du système RAG

 Pourquoi AWS ?

AWS est proposé pour disposer d'une infrastructure cloud :

scalable ;
basée sur des services managés ;
adaptée au déploiement de conteneurs ;
permettant le monitoring ;
avec une facturation à l'utilisation.

L'objectif est de disposer d'une architecture pouvant évoluer avec les besoins de Puls-Events.

Pourquoi Qdrant ?

Le POC utilise FAISS localement.

Pour le MVP, Qdrant Cloud est proposé afin de disposer d'une base vectorielle adaptée à une utilisation plus scalable.

Qdrant permet notamment de combiner la recherche vectorielle avec des filtres sur les métadonnées des événements, ce qui est particulièrement utile pour les critères géographiques.

Backlog

Le backlog est organisé selon la méthode MoSCoW.

Must Have

Fonctionnalités nécessaires au MVP :

mémoire conversationnelle ;
recherche géographique ;
amélioration de la récupération des documents ;
recherche web ;
monitoring ;
déploiement cloud.
Nice to Have

Fonctionnalités pouvant être ajoutées après le MVP :

améliorations supplémentaires du moteur de recherche ;
fonctionnalités avancées de recommandation ;
amélioration du système de reranking.
Estimation
Catégorie	Estimation
Must Have	28 jours
Nice to Have	15 jours
Total	43 jours

Planning

Le projet est planifié sur environ 10 semaines.

Les principales étapes sont :

cadrage du besoin ;
analyse du POC ;
conception de l'architecture ;
définition du backlog ;
planification ;
estimation des coûts ;
analyse du passage POC → MVP ;
préparation de la présentation.

Estimation des coûtsDéveloppement

Estimation :

30 jours × 400 € = 12 000 € HT

Coûts mensuels estimés
Niveau d'utilisation	Coût mensuel estimé
Faible	37 €
Moyen	225 €
Élevé	1 215 €

Ces montants constituent des estimations permettant de comparer les différents niveaux d'exploitation du futur MVP.

POC → MVP

POC	MVP
FAISS local	Qdrant Cloud
Pas de mémoire	Redis
Recherche géographique limitée	Filtres géographiques
Recherche principalement RAG	RAG + recherche web
Monitoring limité	CloudWatch + LangSmith
Streamlit local	API + infrastructure cloud
Prototype	Architecture scalable

Amélioration du RAG

Les résultats RAGAS montrent notamment une faiblesse au niveau du Context Recall.

Plusieurs pistes sont donc proposées :

améliorer les métadonnées ;
utiliser des filtres géographiques ;
améliorer la récupération des documents ;
envisager une recherche hybride ;
envisager du reranking.

L'objectif est d'améliorer progressivement la pertinence des documents récupérés.

Livrables

Ce repository contient notamment :

- le rapport de projet ;
- la présentation ;
- les schémas d'architecture ;
- les éléments de planification ;
- l'estimation des coûts.
- Compétences mobilisées

Ce projet m'a permis de travailler notamment sur :

- le cadrage d'un besoin Data/IA ;
- l'analyse d'un système RAG ;
- l'architecture cloud ;
- la conception d'une solution scalable ;
- la priorisation d'un backlog ;
- la planification d'un projet ;
- l'estimation des coûts ;
- la veille technologique ;
- la justification de choix techniques ;
- la communication professionnelle ;
- la présentation d'une solution à un client.

Compétences acquises pendant le parcours

Ce projet s'appuie également sur les compétences développées lors des projets précédents :

- Python ;
- SQL ;
- MongoDB / NoSQL ;
- ETL ;
- Docker ;
- Spark ;
- Redpanda ;
- Kestra ;
- bases vectorielles ;
- RAG ;
- LangChain ;
- cloud et architecture Data ;
- orchestration des flux.



Auteur : K93000

Projet réalisé dans le cadre de mon parcours : Data Engineer — OpenClassrooms


Portfolio

Ce repository fait partie de mon portfolio Data Engineer et présente une sélection de mes projets réalisés durant ma formation.

Les projets couvrent notamment :

Data Analysis ;
Data Engineering ;
bases de données ;
ETL ;
streaming ;
orchestration ;
RAG et IA générative ;
architecture cloud.
