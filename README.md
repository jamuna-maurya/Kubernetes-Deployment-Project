# Kubernetes Deployment & Auto-Scaling of a Containerized Application

## Project Overview

This project demonstrates the deployment of a containerized full-stack application on Kubernetes using Minikube. The application consists of:

- Frontend (React)
- Backend (Node.js)
- MongoDB Database

Features implemented:

- Kubernetes Deployments
- ReplicaSets
- Services
- Horizontal Pod Autoscaler (HPA)
- Rolling Updates
- Rollback
- Self-Healing
- Monitoring & Logging

---

## Architecture

Frontend (React)
↓
Frontend Service (NodePort / LoadBalancer)
↓
Backend Service (ClusterIP)
↓
Backend Pods (Node.js)
↓
MongoDB Service
↓
MongoDB Pod

---

## Technologies Used

- Docker
- Kubernetes
- Minikube
- kubectl
- React
- Node.js
- MongoDB

---

## Project Structure

Kubernetes-Deployment-Project/

├── frontend/

│ ├── Dockerfile

│ ├── package.json

│ └── src/

├── backend/

│ ├── Dockerfile

│ ├── package.json

│ └── server.js

├── k8s/

│ ├── frontend-deployment.yaml

│ ├── backend-deployment.yaml

│ ├── database-deployment.yaml

│ ├── services.yaml

│ ├── hpa.yaml

│ ├── configmap.yaml

│ └── secret.yaml

└── README.md

---

# Step 1: Start Minikube

```bash
minikube start --driver=docker
kubectl get nodes


Screenshot

NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   2d    v1.35.1


Step 2:Build Docker Images
Frontend

cd frontend
docker build -t <dockerhub-username>/frontend:v1 .


Backend

cd backend
docker build -t <dockerhub-username>/backend:v1 .


Step 3: Push Images

docker push <dockerhub-username>/frontend:v1
docker push <dockerhub-username>/backend:v1


Step 4: Deploy Application

kubectl apply -f k8s/


Screenshot

deployment.apps/frontend created
deployment.apps/backend created
deployment.apps/mongodb created
service/frontend-service created
service/backend-service created
service/mongodb-service created


Step 5: Verify Pods

kubectl get pods


NAME                        READY   STATUS    RESTARTS   AGE
backend-64ddff46f-2cz5n     1/1     Running   0          20m
backend-64ddff46f-q4zmt     1/1     Running   0          20m
frontend-568b8cdbbf-5njr5   1/1     Running   0          43m
frontend-568b8cdbbf-wqcb4   1/1     Running   0          43m
mongodb-8d66f9bd6-zhxhd     1/1     Running   0          63m


Step 6: Verify Deployments

kubectl get deployments


Step 7: Verify ReplicaSets

kubectl get rs

NAME                 DESIRED   CURRENT   READY
backend-64ddff46f    2         2         2
frontend-568b8cdbbf  2         2         2
mongodb-8d66f9bd6    1         1         1


kubectl get svc

NAME               TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
backend-service    ClusterIP      10.100.61.237   <none>        5000/TCP       87m
frontend-service   LoadBalancer   10.103.9.224    <pending>     80:31323/TCP   84m
kubernetes         ClusterIP      10.96.0.1       <none>        443/TCP        2d2h
mongodb-service    ClusterIP      10.99.33.108    <none>        27017/TCP      93m


Step 9: Access Application

minikube service frontend-service --url

curl http://192.168.49.2:31323

output-
<!doctype html>
<html lang="en">
<title>React App</title>
...


Step 10: Configure HPA

kubectl apply -f hpa.yaml
kubectl get hpa


Step 11: Generate Load

kubectl run load-generator \
--image=busybox \
--restart=Never \
-it -- sh

Step 12: Monitor Scaling

kubectl get hpa -w

Step 13: Rolling Update

kubectl set image deployment/backend \
backend=<dockerhub-username>/backend:v2


kubectl rollout status deployment/backend


Step 14: Rollback

kubectl rollout undo deployment/backend


Step 15: Self-Healing

kubectl delete pod <pod-name>

kubectl get pods -w


Step 16: Monitoring & Logs

kubectl logs -l app=frontend


Final Verification

kubectl get pods
kubectl get deployments
kubectl get rs
kubectl get svc
kubectl get hpa
kubectl top pods
```
📷final screenshot-
##<img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/e56b7366-42ae-4c5c-a5cc-361d5a5d65d2" />



##<img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/62ef611f-70f9-47af-8b13-be3cb184ee2a" />


browse -
[http://<your-public-ip>:8080]

##<img width="2764" height="1376" alt="image" src="https://github.com/user-attachments/assets/3f16bd93-2613-40bb-922b-0006ec8c60b6" />


```

Project Outcomes

✅ Kubernetes Deployments

✅ ReplicaSets

✅ Services

✅ Horizontal Pod Autoscaler

✅ Rolling Updates

✅ Rollback

✅ Self-Healing

✅ Monitoring & Logging

✅ React Frontend Deployment

✅ Node.js Backend Deployment

✅ MongoDB Deployment




Author
jeny










