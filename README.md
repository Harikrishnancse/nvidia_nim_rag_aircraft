### **Integrate your Streamlit app with a Kubernetes (K8s) cluster, you'll need to:**

1. Containerize your Streamlit app using the Dockerfile (already done).
2. Push the Docker image to a container registry (like Docker Hub or GCP Container Registry).
3. Create Kubernetes configuration files to deploy your containerized app.
4. Deploy to the Kubernetes cluster using kubectl.

Here’s a detailed step-by-step guide for the Kubernetes integration.

#### **Step 1: Containerize your Streamlit app using the Dockerfile**
##### Build the Docker image
    docker build -t streamlit-nvidia-app .

##### Run the Docker container
    docker run -p 8501:8501 streamlit-nvidia-app
-------------------------------------------------------------------------------------------------------------------------
#### **Step 2: Push the Docker image to a container registry**
If you’re using Docker Hub (replace your-dockerhub-username with your actual Docker Hub username):
    docker tag streamlit-nvidia-app <your-dockerhub-username>/streamlit-nvidia-app:latest

##### Push the image to Docker Hub
    docker push <your-dockerhub-username>/streamlit-nvidia-app:latest

NOTE : If you're using GCP, AWS ECR, or any other registry, follow the respective commands to tag and push the image.
-------------------------------------------------------------------------------------------------------------------------
#### **Step 3: Push the Docker image to a container registry**
##### Create Kubernetes YAML Files
You will need two main files for your Kubernetes deployment:
- **Deployment**: Defines the app (containers, replicas, etc.).
- **Service**: Exposes your app to external users (via LoadBalancer or NodePort).
###### deployment.yaml
This file defines how your containerized Streamlit app will run on the Kubernetes cluster:
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: streamlit-nvidia-app
      labels:
        app: streamlit-nvidia-app
    spec:
      replicas: 2  # Number of pods to run
      selector:
        matchLabels:
          app: streamlit-nvidia-app
      template:
        metadata:
          labels:
            app: streamlit-nvidia-app
        spec:
          containers:
          - name: streamlit-nvidia-app
            image: your-dockerhub-username/streamlit-nvidia-app:latest  # Your pushed Docker image
            ports:
            - containerPort: 8501
            env:
            - name: NVIDIA_API_KEY
              valueFrom:
                secretKeyRef:
                  name: nvidia-api-key-secret
                  key: NVIDIA_API_KEY
    
