### Some important commands to manage argoCD

- Create namespace and install ArgoCD inside k8s cluster.
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

- Get all the services created by argocd
```bash
kubectl get svc -n argocd
```

- Open the argocd-server in GUI inside browser by forwarding port
```bash
kubectl port-forward -n argocd svc/argocd-server 8000:443
```

- Login with a username and password
The initial password for the admin account is auto-generated and stored as clear text in the field password in a secret named argocd-initial-admin-secret in your Argo CD installation namespace. You can simply retrieve this password using kubectl:
```
Default username: admin

- Get password
```
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
![image](https://user-images.githubusercontent.com/73098407/193611367-f3cbccb4-22be-42c0-88eb-46c8f3cf111d.png)

Create a new app and connect your github repo for the configuration file, leave revision as HEAD. If you are using SSH, then make sure you are adding your private key in ```Settings->Repositories```

- Sync the application once it is done.
