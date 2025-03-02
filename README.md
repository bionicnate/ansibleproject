## Executive Summary: IT-Tools and CalibreWeb

This project details the deployment of CalibreWeb and IT-Tools within a local Kubernetes cluster, focusing on secure access and persistent data. CalibreWeb provides a centralized platform for managing and accessing an ebook library, while IT-Tools offers a suite of online utilities. This deployment prioritizes secure access through configured service ports and ensures data persistence using Kubernetes Persistent Volumes. Resource limits are implemented to optimize performance. The deployment aims to create a stable and accessible environment for both ebook management and utility access, leveraging Kubernetes for orchestration and scalability."

## Overview & Deployment Tasks
In this project you will use Ansible to automate the setup and deployment of a multi-container environment on your local machine. Your tasks include:

- **Environment & Tool Installation:**  
    Use Ansible to install Docker, Docker Compose, and K3s (a lightweight Kubernetes distribution).
        - run install-docker-k3s.yml on localhost (inventory.yml)

    ```
    ansible-playbook -i inventory.yml install-docker-k3s.yml    --ask-become-pass
    ```
    
- **Container Management:**  
    Use Ansible to deploy Portainer as a Docker container (running outside the Kubernetes cluster) to manage your containers.
    ```
    ansible -i inventory.yml vm -b -m shell -a "docker volume create portainer_data && docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest" --ask-become-pass
    ```

- **Kubernetes Deployments:**  
    Using Ansible, deploy application services into your K3s cluster via Kubernetes manifest files. 
    ```
    ansible-playbook -i inventory.yml deploymanifests.yaml 
    ```
    ```
    ansible-playbook -i inventory.yml verifyk3s.yml 
    OR
    sudo kubectl get svc -A
    docker ps
    ```

- **Cluster Management Verification:**  
    Deploy a Portainer agent inside the K3s Kubernetes cluster and verify that you can manage the cluster through Portainer.
    ```
    ansible-playbook -i inventory.yml deployportainer.yaml
    ```


This hands-on project will build your skills in containerization, orchestration, and automation while providing real-world experience with Ansible, Docker, and Kubernetes.

