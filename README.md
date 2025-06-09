# k3s-ghrunner-with-sonarqube
Kubernetes K3s setup for GitHub runner and Sonarqube


## Github Runner: Cleanup everything, related to GitHub Runner:

```bash
k3s kubectl delete all,secret,configmap,pvc,ingress -l app=trm-runner-1 -n githubrunner

k3s kubectl delete namespace githubrunner
```

## Github Runner: prepare directories

Create and add necessary permissions for directories:

```bash
mkdir -p /data/runner_logs; chmod 777 /data/runner_logs; mkdir -p /opt/githubrunner/config; chmod 777 /opt/githubrunner/config
```

## Github Runner: apply manifest

```bash
k3s kubectl apply -f github-runner.yaml
```
