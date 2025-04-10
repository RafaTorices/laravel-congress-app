# Laravel-Congress App DEMO
## Description

This is a demo application for the Laravel-Congress project, which is a web application that can be used to manage and display information about congresses, conferences, and other events. The application is built using the Laravel PHP framework and provides a user-friendly interface for managing event data.

## Prerequisites
- **docker**
- **kubectl**
- **kustomize**
- **argoCD**
- **git**
- **php** (for local development)
- **composer** (for local development)
- **node** (for local development)
- **npm** (for local development)
- **laravel** (for local development)
- **phpunit** (for local development)

## Continuous Integration CI
This project uses GitHub Actions for continuous integration (CI) to automate the testing and deployment process. The CI pipeline is configured to run tests and perform other tasks whenever changes are pushed to the repository. This ensures that the codebase remains stable and that any issues are caught early in the development process.

Workflows are defined in the `.github/workflows` directory, and you can customize them to fit your project's needs. The CI pipeline includes steps for running tests, checking code quality, and deploying the application to a staging or production environment.

- **Tests**: The application includes a suite of tests to ensure that the code is functioning as expected. These tests are run automatically as part of the CI pipeline.
- **Quality**: The CI pipeline includes steps to check the code quality using tools like PHPStan and PHP CS Fixer. This helps maintain a clean and consistent codebase.
- **Deploy**: The CI pipeline can be configured to automatically deploy the application to a staging or production environment whenever changes are pushed to the repository. This ensures that the latest version of the application is always available to users.

### Gitflow
This project follows the Gitflow branching model, which is a popular branching strategy for Git. The main branches in this project are:
- **main**: This branch contains the production-ready code. It is the default branch and should always be in a deployable state.
- **develop**: This branch contains the latest development code. It is where new features and bug fixes are merged before being released to production.
- **feature/**: These branches are used for developing new features. They are created from the `develop` branch and merged back into `develop` when the feature is complete.
- **bugfix/**: These branches are used for fixing bugs. They are created from the `develop` branch and merged back into `develop` when the bug is fixed.
- **release/**: These branches are used for preparing a new release. They are created from the `develop` branch and merged into both `main` and `develop` when the release is ready.
- **hotfix/**: These branches are used for fixing critical bugs in the production code. They are created from the `main` branch and merged back into both `main` and `develop` when the hotfix is complete.

## Kubernetes
This project uses Kubernetes for container orchestration. In folder `k8s/` you can find the Kubernetes manifests for deploying the application. The manifests are organized into different directories based on the `kustomize` environment. The `kustomize` tool is used to manage the Kubernetes manifests and allows for easy customization of the deployment process.

To deploy the application to a Kubernetes cluster, you need to have a Kubernetes cluster set up and configured. You can use tools like Minikube or Kind for local development, or you can use a cloud provider like AWS, GCP, or Azure for production deployments.

Executing the following command will create the Kubernetes resources defined in the manifests:

```bash
kubectl apply -f k8s/app/base/
```
This command will create the necessary resources, such as deployments, services, and ingress rules, to run the application in the Kubernetes cluster.


### Kustomize
There are two main directories in the `k8s/` folder:
- **base/**: This directory contains the base Kubernetes manifests for the application. These manifests are used as a starting point for creating different environments (dev and prod).
- **overlays/**: This directory contains the overlay manifests for different environments. Each environment has its own directory (`dev/`, `prod/`) that contains the specific configuration for that environment.

To deploy the application `dev` using `kustomize`, you can use the following command:

```bash
kubectl apply -k k8s/app/overlays/dev/
```
To deploy the application `prod` using `kustomize`, you can use the following command:

```bash
kubectl apply -k k8s/app/overlays/prod/
```


## Continuous Deployment CD - ArgoCD
This project uses ArgoCD for continuous deployment (CD) to automate the deployment process. Whenever changes are pushed to the `main` branch, ArgoCD automatically deploys the latest version of the application to the production environment. This ensures that the latest version of the application is always available to users.

Previously, you need to install ArgoCD in your Kubernetes cluster. You can do this by running the following command:

```bash
# Install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

To access the ArgoCD dashboard, you can use the following command to port-forward the ArgoCD server to your local machine:

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Then, you can access the ArgoCD dashboard by navigating to `https://localhost:8080` in your web browser. The default username is `admin`, and the password can be obtained using the following command:

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 -d
```

### To access the application, you can access to the ingress URL:
In local environment, you can access the application using the following URL:
```
http://localhost
```

