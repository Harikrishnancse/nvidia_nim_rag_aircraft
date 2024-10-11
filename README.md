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

#### **Step 2: Push the Docker image to a container registry**
If you’re using Docker Hub (replace your-dockerhub-username with your actual Docker Hub username):
    docker tag streamlit-nvidia-app <your-dockerhub-username>/streamlit-nvidia-app:latest
##### Push the image to Docker Hub
    docker push <your-dockerhub-username>/streamlit-nvidia-app:latest

NOTE : If you're using GCP, AWS ECR, or any other registry, follow the respective commands to tag and push the image.

