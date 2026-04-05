## Task 1: Core Concepts

```yml
Helm simplifies Kubernetes by managing the complexity of multiple related manifests.

Chart: A directory containing the templates for your K8s resources.

Release: An instance of a Chart running in a cluster. You can have multiple releases of the same chart (e.g., prod-db and dev-db).

Repository: Where charts are stored and shared.

Verification: Run helm version. You are likely running version v3.x.x, which is the current standard and notably "Tiller-less" (more secure than v2).
```

## Task 2 & 3: Repositories and Installation

```yml
Instead of writing 100 lines of YAML for an Nginx setup with high availability, we use a trusted source like Bitnami.

Action: ```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install my-nginx bitnami/nginx

Observation: kubectl get all shows that Helm automatically created a Deployment, Service, and potentially a Secret/ConfigMap.

Verification: By default, Bitnami's Nginx usually starts 1 Pod and uses a LoadBalancer service type (which might stay <pending> on local clusters like Minikube/Kind unless a tunnel is running).
```

## Task 4: Customizing with Values

The power of Helm lies in the values.yaml file, which feeds data into the templates.

Method A: The --set flag (Quick overrides)

```yml
helm install quick-nginx bitnami/nginx --set replicaCount=3 --set service.type=NodePort
```

Method B: The values file (Production standard)

```yml
# custom-values.yaml

replicaCount: 2
service:
  type: ClusterIP
resources:
  limits:
    cpu: 100m
    memory: 128Mi
```

Install: helm install custom-nginx bitnami/nginx -f custom-values.yaml

## Task 5: Upgrade and Rollback

```yml
Helm tracks every change to a release as a Revision.

Upgrade: helm upgrade my-nginx bitnami/nginx --set replicaCount=5

History: helm history my-nginx (You will see Revision 1 and 2).

Rollback: helm rollback my-nginx 1

Verification: After rolling back, helm history will show Revision 3. Revision 3 is a mirror of Revision 1. Helm never deletes history; it only moves forward.
```

## Task 6: Creating a Custom Chart

```yml
When you run helm create my-app, Helm scaffolds a standard directory structure.

The Template Engine:
Inside templates/deployment.yaml, you will see code like:
replicas: {{ .Values.replicaCount }}

This tells Helm: "Go to values.yaml, find the replicaCount key, and inject its value here."

Validate: helm lint my-app checks for syntax errors.

Dry Run: helm template my-release ./my-app shows you the raw YAML that would be sent to Kubernetes without actually installing it.
```

## Task 7: Clean Up

```yml
helm uninstall my-nginx
helm uninstall quick-nginx
helm uninstall custom-nginx
helm uninstall my-release
rm -rf my-app custom-values.yaml
```

---
