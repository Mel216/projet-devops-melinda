# Guide des Captures d'Écran pour Melinda AMRI

Voici le guide précis pour réaliser les 27 captures d'écran demandées par votre professeur, en lien avec les fichiers de votre projet.

### Partie 1 : Jenkins & Infrastructure (CI)
| Capture | Description | Source / Fichier |
| :--- | :--- | :--- |
| **1** | Interface de connexion | Accès web `localhost:8010` |
| **2** | Plugins installés | Dashboard Jenkins > Administrer Jenkins > Plugins |
| **3** | Credentials | Dashboard Jenkins > Administrer Jenkins > Credentials |
| **4** | Config SonarQube | Dashboard Jenkins > Administrer Jenkins > System > SonarQube servers |
| **5** | Dashboard SonarQube | Accès web `localhost:9091` (après le premier build) |
| **6** | **Code Jenkinsfile** | Fichier `Jenkinsfile` (Lignes 1 à 60) |
| **7** | Stage View | Vue de votre Job Jenkins après succès |
| **8** | DockerHub | Votre compte sur hub.docker.com (Image `demo-java-app`) |

### Partie 2 : Kubernetes & ArgoCD (CD)
| Capture | Description | Commande / Fichier |
| :--- | :--- | :--- |
| **9** | État Minikube | Terminal : `minikube status` |
| **10** | Namespaces | Terminal : `kubectl get ns` |
| **11** | Dossier Helm | Explorateur de fichiers : Dossier `helm/app/` |
| **12** | **Update Tag** | Fichier `helm/app/values.yaml` (Ligne 8 : `tag: "V1.0"`) |
| **13** | Interface ArgoCD | Accès web `localhost:30080` |
| **14** | App Health | Dashboard ArgoCD (Application `demo-java-app`) |
| **15** | Accès App Web | Navigateur : Résultat de `minikube service demo-java-app-service` |

### Partie 3 : Observabilité (Monitoring & Logging)
| Capture | Description | Commande / Fichier |
| :--- | :--- | :--- |
| **16** | Prometheus Targets | Accès web `localhost:9090` > Status > Targets |
| **17** | Grafana Login | Accès web `localhost:30040` |
| **18** | Dashboard Grafana | Dashboard importé sur Grafana |
| **19** | Service Elastic | Terminal : `kubectl get svc -n logging` |
| **20** | Home Kibana | Accès web `localhost:30056` |
| **21** | Logs Kibana | Menu "Discover" dans Kibana |

### Partie 4 : Modification & Pipeline Automatique
| Capture | Description | Fichier / Action |
| :--- | :--- | :--- |
| **22** | **Modif Code** | Fichier `demo-java-app/src/main/resources/templates/index.html` (Ligne 50) |
| **23** | Git Push | Terminal : `git add . && git commit -m "update" && git push` |
| **24** | Auto trigger | Dashboard Jenkins montrant le build #2 lancé automatiquement |
| **25** | Sync ArgoCD | Dashboard ArgoCD montrant le passage de "Out of Sync" à "Synced" |
| **26** | Résultat Final | Navigateur affichant la version **v2.0** de l'app |
| **27** | Diagramme Flux | Utilisez le schéma du PDF ou Mermaid |
