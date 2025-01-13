# DevOps Mini-Projet : Conteneurisation, Orchestration et Monitoring d'une Application Web

## 1. Introduction
Ce projet DevOps consiste à conteneuriser, orchestrer et surveiller une application web développée par l'étudiant. L'application sera déployée sur un cluster Kubernetes local (par exemple Minikube). Un système de monitoring avec Prometheus et Grafana sera mis en place pour collecter et visualiser les métriques.

---

## 2. Objectifs
- **Conteneurisation** : Utiliser Docker pour empaqueter l'application.
- **Orchestration** : Déployer l'application sur Kubernetes.
- **Monitoring** : Intégrer Prometheus et Grafana pour observer l'application.

---


### 3.1. Conteneurisation
- **App** : Conteneur principal exposé sur le port `5000`.
- **MySQL** : Base de données, exposée sur le port `3306`.

### 3.2. Orchestration Kubernetes
- Deployments et Services pour la gestion des pods.
- ConfigMap et Secrets pour les configurations sensibles.
- ![Capture d'écran 2025-01-11 000840](https://github.com/user-attachments/assets/1166466a-e18f-4de8-96ef-ed444f7ea14f)

### 3.3. Intégration Continue
- Pipeline Jenkins pour automatiser les tâches DevOps.
- Construction, scan de vulnérabilités, et push des images Docker.

- ![Capture d'écran 2025-01-13 220120](https://github.com/user-attachments/assets/43ab252e-976d-4990-bb1d-e28d7ba7efe8)
- ![Capture d'écran 2025-01-12 004442](https://github.com/user-attachments/assets/ffe5b13a-3f4b-499a-a47e-cf3fef26ddba)


### 3.4. Helm Charts et GitOps
- **Helm Charts** :simplifier et organiser le déploiement des ressources Kubernetes.
- **ArgoCD** : une stratégie GitOps pour un déploiement automatisé et synchrone via un dépôt Git
- ![Capture d'écran 2025-01-13 010123](https://github.com/user-attachments/assets/04fa8f8c-8b6d-4549-8da4-b0ce58de596a)

### 3.5. Monitoring et Observabilité
- **Prometheus** : Collecte les métriques.
- **Grafana** : Visualisation des métriques avec des tableaux de bord.
- ![Capture d'écran 2025-01-13 010026](https://github.com/user-attachments/assets/8c70b97d-9cdd-4102-90dc-9e15a56ff87b)

---

## 4. Instructions de Déploiement

### 4.1. Prérequis
- Installer Docker, Docker Compose, Kubernetes, Minikube et Helm.

### 4.2. Conteneurisation
Exécutez les commandes suivantes pour construire et exécuter le conteneur :
```bash
docker build -t inessbk/myapp-backend:latest .
docker-compose up

```

### 4.2. Monitoring avec Prometheus et Grafana
- Installez Prometheus et Grafana avec Helm :

```bash
   helm install prometheus prometheus-community/prometheus    --namespace monitoring
   helm install grafana prometheus-community/grafana --namespace monitoring
   ```
---

### 4.3. Déploiement Kubernetes
Lancez les commandes suivantes pour déployer sur Minikube :
```bash
minikube start
kubectl apply -f k8s/
helm install gestion-formation ./helm-chart
```
### 4.4. Monitoring avec Prometheus et Grafana
Installez Prometheus et Grafana avec Helm :

```bash
helm install prometheus prometheus-community/prometheus --namespace monitoring
helm install grafana prometheus-community/grafana --namespace monitoring
```
---


