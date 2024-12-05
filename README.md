# cosmocloud-deploy
#Cosmocloud-Deploy
Cosmocloud-Deploy is a Helm chart designed to deploy a backend, frontend, and Redis for a cloud-native application. This project simplifies the deployment of these components using Kubernetes.

Helm Chart Details
Chart Name: cosmocloud-deploy
Chart Version: 1.0.0
App Version: 1.0.0
Type: Application
#Components Deployed:
Backend
Frontend
Redis
#Deployment Structure
#1. Backend
Deployment File: backend-deployment.yml
Service File: backend-service.yml
ConfigMap: Holds REDIS_URI for backend communication with Redis.
#Key Details:

Image: shreybatra/sample-backend
Port: 8000
Environment Variable:
REDIS_URI: redis://redis-svc:6379
#2. Frontend
Deployment File: frontend-deployment.yml
Service File: frontend-service.yml
ConfigMap: Holds BACKEND_URL for frontend communication with the backend.
#Key Details:

Image: shreybatra/sample-frontend
Port: 5175
NodePort: 31000
Environment Variable:
BACKEND_URL: http://backend-svc:8000
#3. Redis
Deployment File: redis-deployment.yml
Service File: redis-service.yml
#Key Details:

Image: redis
Port: 6379
Installation
Prerequisites
Kubernetes Cluster
Helm installed on your system
Steps
Clone the repository:

bash
Copy code
git clone https://github.com/chakri-592/cosmocloud-deploy.git
cd cosmocloud-deploy
Deploy the Helm chart:

bash
Copy code
helm install cosmocloud ./cosmocloud-deploy
Verify the deployment:

bash
Copy code
kubectl get all
Configuration
Values File (Values.yml)
Adjust the following configurations as needed:

Namespace: Specify the namespace for deployments.
Service Types: Update service types (e.g., NodePort, ClusterIP).
Accessing the Application
Frontend: Accessible via NodePort at http://<NODE_IP>:31000.
Backend: Internally accessible at http://backend-svc:8000.
Redis: Internally accessible at redis://redis-svc:6379.
Project Structure
plaintext
Copy code
cosmocloud-deploy/
│
├── templates/
│   ├── backend-deployment.yml
│   ├── backend-service.yml
│   ├── frontend-deployment.yml
│   ├── frontend-service.yml
│   ├── redis-deployment.yml
│   ├── redis-service.yml
│
├── Chart.yaml
├── README.md
├── Values.yml
License
This project is licensed under the MIT License.
