# MedifyDevOps - Flask App Deployment on Minikube

This project demonstrates how to containerize a Flask web application using Docker and deploy it on Kubernetes using Minikube.

## Prerequisites
Before you begin, ensure you have the following installed:
- [Python 3](https://www.python.org/downloads/)
- [Docker](https://www.docker.com/get-started)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Git](https://git-scm.com/downloads/)

## Project Structure
```
medifyDevOps/
│── app.py              # Flask application
│── Dockerfile         # Docker configuration file
│── deployment.yaml   # Kubernetes Deployment manifest
│── service.yaml       # Kubernetes Service manifest
│── requirements.txt  # Python dependencies
│── screenshots/      # Deployment proof (screenshots)
│── README.md         # Documentation
```

## Step 1: Clone the Repository
```sh
git clone https://github.com/zuzu-18/medifyDevOps.git
cd medifyDevOps
```

## Step 2: Build and Run the Flask App Locally
```sh
pip install -r requirements.txt
python app.py
```
Test in a browser at: [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

## Step 3: Build and Run the Docker Container
```sh
docker build -t flask-app:latest .
docker run -p 5000:5000 zuzu18/flask-app:latest
```
Test in a browser at: [http://localhost:5000/](http://localhost:5000/)

```
### Apply tag and Push already built Docker Image to Docker Hub
```sh
docker tag flask-app:latest zuzu18/flask-app:latest
docker push zuzu18/flask-app:latest

```
## Step 4: Deploy to Minikube
### Start Minikube
```sh
minikube start
### Load Docker Image into Minikube
```sh
minikube image load zuzu18/flask-app:latest
```
### Apply Kubernetes Manifests
```sh
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
### Verify Deployment
```sh
kubectl get pods
kubectl get services
```

## Step 5: Access the Flask App in Minikube
Find the service URL:
```sh
minikube service flask-service --url
```
Copy the URL and open it in a browser or use:
```sh
curl <MINIKUBE_URL>
```
### Expected output:
```sh
Welcome to DevOps Flask App!
```

## Step 6: Push to GitHub
```sh
git init
git remote add origin https://github.com/zuzu-18/medifyDevOps.git
git add .
git commit -m "feat: create Flask app, containerize with Docker, deploy on Minikube"
git push origin main
```

## Step 7: Provide Deployment Proof
Take screenshots of:
- Running Minikube cluster (`minikube status`)
- Running pods (`kubectl get pods`)
- Service exposing the application (`kubectl get services`)
- Curl command output (`curl <MINIKUBE_URL>`)
- Browser output showing *Welcome to DevOps Flask App!*
