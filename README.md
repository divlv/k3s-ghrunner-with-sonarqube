# k3s-ghrunner-with-sonarqube
Kubernetes K3s setup for GitHub runner and Sonarqube

## Github Runner

### Github Runner: Cleanup everything, related to GitHub Runner:

```bash
k3s kubectl delete all,secret,configmap,pvc,ingress -l app=trm-runner-1 -n githubrunner

k3s kubectl delete namespace githubrunner
```

### Github Runner: prepare directories

Create and add necessary permissions for directories:

```bash
mkdir -p /data/runner_logs; chmod 777 /data/runner_logs; mkdir -p /opt/githubrunner/config; chmod 777 /opt/githubrunner/config
```

### Github Runner: apply manifest

```bash
k3s kubectl apply -f github-runner.yaml
```

### Github Runner: Check the logs

```bash
k3s kubectl -n githubrunner logs -f deploy/trm-runner-1
```

## Sonarqube

### Sonarqube: create namespace

```bash
k3s kubectl create namespace sonarqube
```

### Sonarqube: prepare directories
```bash
mkdir -p /data/postgres; chmod 777 /data/postgres; mkdir -p /data/sonarqube; chmod 777 /data/sonarqube; mkdir -p /data/sonarqube/cbp/plugins; chmod 777 /data/sonarqube/cbp/plugins; mkdir -p /data/sonarqube/cbp/web; chmod 777 /data/sonarqube/cbp/web
```

### Sonarqube: Integration plugins

Unpack the Sonarqube Community Branch Plugin and Sonarqube Webapp plugin:

```bash
sudo cp sonarqube-community-branch-plugin-25.5.0.jar /data/sonarqube/cbp/plugins/

sudo unzip -q sonarqube-webapp.zip -d /data/sonarqube/cbp/web
```





### Sonarqube: apply commands (to be refined)

```bash
k3s kubectl apply -f pg-sonar-secrets.yaml

k3s kubectl apply -f postgres-pv.yaml
k3s kubectl apply -f postgresql-headless-svc.yaml
k3s kubectl apply -f postgres-statefulset.yaml

k3s kubectl apply -f sonardata-pv.yaml
k3s kubectl apply -f sonarqube.yaml
```


### Sonarqube: restart deployment if needed

After applying/editing the configuration, you may need to restart the SonarQube deployment to ensure it picks up the new settings and secrets:
```bash
k3s kubectl apply -f sonarqube.yaml
k3s kubectl -n sonarqube rollout restart deploy/sonarqube
```


## HTTPS access to Sonarqube

**ATTENTION!** Valid SSL certificate is required, because, otherwise, GitHub Actions will not be able to connect to Sonarqube (due to security reasons).

### Traefik: prepare directories

```bash
mkdir -p /opt/traefik-data; chmod 777 /opt/traefik-data
```

### Traefik: ...

To be continued...
