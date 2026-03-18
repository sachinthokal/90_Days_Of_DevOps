### Task 1: Explore Default Namespaces

```yml
kubectl get namespaces

kubectl get pods -n kube-system

```

![alt text](image.png)

### Task 2: Create and Use Custom Namespaces

```yml
kubectl create namespace dev
kubectl create namespace staging


kubectl run nginx-dev --image=nginx:latest -n dev
kubectl run nginx-staging --image=nginx:latest -n staging

kubectl get pods -A

```

![alt text](image-1.png)

![alt text](image-2.png)

![alt text](image-3.png)

---

### Task 3: Create Your First Deployment

```yml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: dev
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.24
        ports:
        - containerPort: 80

```

![alt text](image-4.png)

### Task 4: Self-Healing — Delete a Pod and Watch It Come Back

```yml
# List pods
kubectl get pods -n dev

# Delete one of the deployment's pods (use an actual pod name from your output)
kubectl delete pod <pod-name> -n dev

# Immediately check again
kubectl get pods -n dev

```

![alt text](image-5.png)

### Task 5: Scale the Deployment

```yml

# Scale up to 5
kubectl scale deployment nginx-deployment --replicas=5 -n dev
kubectl get pods -n dev

# Scale down to 2
kubectl scale deployment nginx-deployment --replicas=2 -n dev
kubectl get pods -n dev

```

![alt text](image-6.png)

---

### Task 6: Rolling Update

```yml

kubectl set image deployment/nginx-deployment nginx=nginx:1.25 -n dev

kubectl rollout status deployment/nginx-deployment -n dev

kubectl rollout history deployment/nginx-deployment -n dev

kubectl rollout undo deployment/nginx-deployment -n dev
kubectl rollout status deployment/nginx-deployment -n dev

kubectl describe deployment nginx-deployment -n dev | grep Image

```

Before rollout back image nginx:1.25 [ on latest version]

![alt text](image-7.png)

After rollout new image nginx:1.24 [ on old version]

![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

![alt text](image-12.png)

---
