# Passez votre système IA du POC au MVP — Puls-Events 🚀

Ce dépôt contient le dossier de cadrage et la documentation technique permettant de faire évoluer le système IA de **Puls-Events** d'un Proof of Concept (POC) vers un Minimum Viable Product (MVP) basé sur une architecture **RAG** (Génération Augmentée par Récupération).

---

## 📄 Document du projet


 **[Consulter le Rapport de Gestion de Projet complet (PDF)](./Rapport_de_gestion_de_projet.pdf)**

---

## 🏛️ Aperçu de l'Architecture Technique Cible

- **Backend / Orchestration :** FastAPI sur **AWS ECS Fargate**
- **Point d'entrée :** **Amazon API Gateway**
- **Base Vectorielle :** **Qdrant Cloud** (recherche sémantique & filtres géographiques)
- **Modèle de Langage (LLM) :** **Mistral AI**
- **Mémoire Conversationnelle :** **Amazon ElastiCache for Redis**
- **Agent Complémentaire :** **smolagents** (recherche Web si besoin)
- **Source de Données :** **OpenAgenda**
- **Observabilité :** **Amazon CloudWatch** & **LangSmith**