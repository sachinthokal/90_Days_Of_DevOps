### Task 1: Deploy the Application

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
  labels:
    app: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.25
        ports:
        - containerPort: 80


# kubectl apply -f app-deployment.yaml
# kubectl get pods -o wide

```

![alt text](image.png)

---

### Task 2: ClusterIP Service (Internal Access)

```yml
apiVersion: v1
kind: Service
metadata:
  name: web-app-clusterip
spec:
  type: ClusterIP
  selector:
    app: web-app
  ports:
    - port: 80
      targetPort: 80

```

![alt text](image-1.png)

---

### Task 3: Discover Services with DNS

![alt text](image-2.png)

### Task 4: NodePort Service (External Access via Node)

![alt text](image-3.png)

![alt text](image-4.png)

---

```yml

# loadbalancer-service.yaml

apiVersion: v1
kind: Service
metadata:
  name: web-app-loadbalancer
spec:
  type: LoadBalancer
  selector:
    app: web-app
  ports:
  - port: 80
    targetPort: 80

```

### Task 6: Understand the Service Types Side by Side

![alt text](image-5.png)
