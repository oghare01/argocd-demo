# Learning  how to deploy applicatons in kubernetes using the GITOPS approach

GitOps is an approach in DevOps that uses Git as a single source of truth for managing infrastructure and application configurations, promoting continuous deployment and operations. ArgoCD is a tool that implements GitOps principles specifically for Kubernetes, providing automated synchronization, visualization, and self-healing capabilities.

## How is GitOps related to ArgoCD?
ArgoCD is a popular tool used to implement GitOps for Kubernetes. It provides the following features that align with GitOps principles:

1. **Continuous Synchronization**: ArgoCD continuously monitors the Git repository for changes and ensures that the state of the Kubernetes cluster matches the desired state defined in the repository. If it detects any drift, it can automatically or manually synchronize the cluster back to the desired state.

2. **Declarative Setup**: Applications are defined declaratively, and ArgoCD uses these definitions to manage the deployment and lifecycle of applications on Kubernetes.

3. **Visual Interface**: ArgoCD provides a web-based user interface and CLI for visualizing the state of applications, making it easier to understand and manage the state of the cluster.

4. **Self-Healing**: By continuously ensuring the cluster state matches the desired state, ArgoCD helps in maintaining the integrity and stability of the system. It can automatically correct any deviations from the desired state.

5. **Integration with Git:** ArgoCD directly integrates with Git repositories, enabling it to watch for changes and apply them to the Kubernetes cluster as soon as they are detected

Here are the steps to install ArgoCD and retrieve the admin password:

1. **Create Namespace for ArgoCD**:
   ```bash
   kubectl create namespace argocd
   ```

2. **Apply ArgoCD Manifests**:
   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

3. **Patch Service Type to LoadBalancer**:
   ```bash
   kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
   ```

4. **Retrieve Admin Password**:
    ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

These commands will install ArgoCD into the specified namespace, set up the service as a LoadBalancer, and retrieve the admin password for you to access the ArgoCD UI.
   ```
