## Task 1 & 2: Metrics Server & kubectl top

```
The Metrics Server is a cluster-wide aggregator of resource usage data. It collects metrics like CPU and memory from the summary API, exposed by the Kubelet on each node.

Installation (Minikube): minikube addons enable metrics-server

Verification: Run kubectl top nodes.

Observation: You will see the CPU(cores) and MEMORY(bytes) currently being consumed. Note that kubectl top shows actual usage, whereas kubectl describe shows reserved (requested) usage.

```

## Task 3: The Scalable Deployment

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-apache
spec:
  selector:
    matchLabels:
      run: php-apache
  replicas: 1
  template:
    metadata:
      labels:
        run: php-apache
    spec:
      containers:
      - name: php-apache
        image: registry.k8s.io/hpa-example
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: 200m
---
apiVersion: v1
kind: Service
metadata:
  name: php-apache
spec:
  ports:
  - port: 80
  selector:
    run: php-apache
```

---

## Task 4 & 5: Imperative HPA and Load Testing

```python
We tell Kubernetes: "Keep the average CPU across all pods at 50% of their request (100m)."Command: kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10Generate Load: ```bashkubectl run load-generator --image=busybox:1.36 --restart=Never -- /bin/sh -c "while true; do wget -q -O- http://php-apache; done"The Math: If your pod hits 400m CPU usage, and your target is 50% of 200m (which is 100m), the HPA calculates:$$desiredReplicas = \lceil 1 \times (400m / 100m) \rceil = 4 \text{ replicas}$$
```

## Task 6: Declarative HPA (v2)

```yml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: php-apache
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: php-apache
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 100
        periodSeconds: 15
    scaleUp:
      stabilizationWindowSeconds: 0
      policies:
      - type: Percent
        value: 100
        periodSeconds: 15
```

## Task 7: Clean Up

```yml
kubectl delete hpa php-apache
kubectl delete deployment php-apache
kubectl delete service php-apache
kubectl delete pod load-generator
```
