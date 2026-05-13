# minikube-ArgoCD
# Create namespace & install ArgoCD
kubectl create namespace argocd

kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Wait for pods to be ready
kubectl wait --for=condition=Ready pods --all -n argocd --timeout=120s

# Expose the ArgoCD UI in the background
kubectl port-forward svc/argocd-server -n argocd 8080:443 &

# Kill the Process Later
pkill -f "port-forward svc/argocd-server"

# Retrieve the Admin Password
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
