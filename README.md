## Deployment steps
1. start the Minikube cluster: 'minikube start --driver=docker'
2. build Docker image: 'docker build-t your-image-name.'
3. Push the image to Docker Hub or other image repository.
4. Deploy applications:
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
5. Verify that the application is running
kubectl get pods
6. Access the application: minikube service node-app-service