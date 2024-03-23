# crud-app-k8s-manifest

#### Overview:

This repository stores Kubernetes manifests for deploying the CRUD application. It includes configurations for deploying the PHP application, MySQL database, ConfigMap, Secrets, and other necessary resources. The Jenkins pipeline defined here updates the Kubernetes manifests automatically whenever there is a change in the Docker images pushed to Docker Hub by the CI/CD pipeline in the `crud-app` repository.

#### Project Structure:

-   adminer-svc.yaml: Kubernetes Service configuration for Adminer.
-   app-deploy.yaml: Deployment configuration for the PHP application.
-   configmap.yaml: ConfigMap configuration for storing environment variables.
-   db-deploy.yaml: Deployment configuration for the MySQL database.
-   secrets.yaml: Secrets configuration for sensitive data.
-   Jenkinsfile: Jenkins pipeline for updating Kubernetes manifests.

#### Jenkins Pipeline:

1.  Checkout Source: This stage fetches the Kubernetes manifests from the repository.
2.  Update GIT: Modifies the `app-deploy.yaml` file to update the Docker image tag with the latest version built by the CI/CD pipeline in the `crud-app` repository. Then, it commits and pushes the changes back to the repository.

These two repositories together form a GitOps pipeline where changes made to the application trigger automated CI/CD processes, ensuring efficient and reliable deployment of the CRUD application on Kubernetes.

CRUD App Repository: [crud-app-k8s-manifest](https://github.com/aymenzarour/crud-app)
