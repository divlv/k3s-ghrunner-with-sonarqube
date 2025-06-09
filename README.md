# k3s-ghrunner-with-sonarqube
Kubernetes K3s setup for GitHub runner and Sonarqube


## Cleanup everything, related to GitHub Runner:

```bash
k3s kubectl delete all,secret,configmap,pvc,ingress -l app=trm-runner-1 -n githubrunner
```
