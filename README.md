# minikube-ArgoCD
# Create namespace & install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f \
  https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Wait for pods to be ready
kubectl wait --for=condition=Ready pods --all -n argocd --timeout=120s

# Expose the ArgoCD UI
kubectl port-forward svc/argocd-server -n argocd 8080:443



$$$
minikube service demo-app-svc