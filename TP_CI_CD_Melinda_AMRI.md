# Rapport de Projet CI/CD & DevOps
**Nom :** AMRI  
**Prénom :** Melinda  
**Sujet :** Automatisation du Pipeline CI/CD pour une application Spring Boot avec Observabilité.

---

## Introduction
Ce projet consiste en la mise en place d'une chaîne de production logicielle automatisée (Pipeline CI/CD) suivant les principes du DevOps. L'objectif est de garantir une livraison continue, de haute qualité, tout en assurant une visibilité totale sur l'état de l'application et de l'infrastructure via des outils de monitoring et de logging.

---

## Partie 1 : Continuous Integration (CI) - Jenkins & Maven

Dans cette phase, nous avons configuré l'environnement de build et d'analyse. Jenkins sert d'orchestrateur principal.

### 1.1 Infrastructure Jenkins
Nous avons utilisé Docker Compose pour déployer Jenkins et SonarQube. Le Dockerfile de Jenkins a été personnalisé pour inclure Maven, Docker CLI et les certificats nécessaires.

> **[Capture 1 : Interface de connexion Jenkins]**
> ![Capture 1](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture1_jenkins_login.png)
> *Description : L'interface d'accueil de Jenkins après configuration initiale.*

> **[Capture 2 : Liste des plugins installés]**
> ![Capture 2](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture2_jenkins_plugins.png)
> *Description : Plugins installés : Docker Pipeline, SonarQube Scanner, Maven Integration.*

### 1.2 Analyse de Code Statique (SonarQube)
Le pipeline exécute `mvn sonar:sonar` pour envoyer le code vers SonarQube. L'analyse vérifie les bugs, les vulnérabilités et la couverture de code.

> **[Capture 5 : Dashboard SonarQube]**
> ![Capture 5](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture5_sonarqube_dashboard.png)
> *Description : Résultats de l'analyse montrant un "Quality Gate" Vert.*

### 1.3 Pipeline Jenkins
Le `Jenkinsfile` contient 5 étapes majeures : Checkout, Build, Analysis, Docker Push, et Update Helm.

> **[Capture 7 : Exécution du pipeline]**
> ![Capture 7](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture7_pipeline_view.png)
> *Description : Vue "Stage View" de Jenkins montrant toutes les étapes en succès.*

---

## Partie 2 : Continuous Deployment (CD) - Kubernetes & ArgoCD

Nous utilisons une approche GitOps pour le déploiement sur un cluster Kubernetes (Minikube).

### 2.1 Cluster Kubernetes (Minikube)
Le cluster est divisé en namespaces pour isoler l'application, les outils de monitoring et de logging.

> **[Capture 10 : Liste des namespaces]**
> ![Capture 10](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture10_namespaces.png)
> *Description : Sortie de la commande `kubectl get ns`.*

### 2.2 Helm Charts
L'application est packagée sous forme de Helm Chart pour faciliter la gestion des versions et des configurations.

> **[Capture 12 : Mise à jour du tag image]**
> ![Capture 12](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture12_helm_values.png)
> *Description : Fichier `values.yaml` après mise à jour automatique du tag par Jenkins.*

### 2.3 GitOps avec ArgoCD
ArgoCD assure que l'état du cluster correspond exactement à ce qui est défini dans le dépôt Git.

> **[Capture 14 : État ArgoCD]**
> ![Capture 14](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture14_argocd_sync.png)
> *Description : Dashboard ArgoCD montrant l'application au statut "Synced" et "Healthy".*

---

## Partie 3 : Observabilité - Monitoring & Logging

### 3.1 Monitoring (Prometheus & Grafana)
Nous suivons les métriques de performance. Prometheus collecte les données et Grafana les visualise.

> **[Capture 18 : Dashboard Grafana]**
> ![Capture 18](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture18_grafana_metrics.png)
> *Description : Graphiques montrant l'utilisation CPU et Mémoire des Pods.*

### 3.2 Logging (ELK Stack)
Les logs sont collectés par Filebeat, stockés dans Elasticsearch et visualisés dans Kibana.

> **[Capture 21 : Visualisation Kibana]**
> ![Capture 21](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture21_kibana_logs.png)
> *Description : Recherche "Discover" dans Kibana filtrant les logs de l'application.*

---

## Partie 4 : Test de Modification & Pipeline Automatique

Nous avons modifié le fichier `index.html` pour passer à la version **v2.0**.

> **[Capture 26 : Nouvelle version visible]**
> ![Capture 26](file:///Users/melindaamri/Downloads/projet_devops_melinda_amri/screenshots/capture26_app_v2.png)
> *Description : Navigateur affichant le message mis à jour après déploiement automatique.*

---

## Conclusion
Le projet est un succès. Nous avons automatisé le cycle complet, de la modification du code jusqu'au monitoring en production, garantissant ainsi fiabilité et rapidité.
