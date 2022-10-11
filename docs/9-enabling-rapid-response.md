* Explain what rapid response does

* Install it

```
export SYSDIG_ACCESS_KEY="xxx"
export SAAS_REGION="eu1"
export API_ENDPOINT="eu1.app.sysdig.com"
export PASSPHRASE=$(openssl rand -base64 32)

helm repo list | grep -q sysdig || helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install rapid-response sysdig/rapid-response \
  --namespace sysdig-rapid-response \
  --create-namespace \
  --set sysdig.accessKey=${SYSDIG_ACCESS_KEY} \
  --set rapidResponse.passphrase=${PASSPHRASE} \
  --set rapidResponse.apiEndpoint=${API_ENDPOINT} \
  --set 'rapidResponse.extraVolumes.volumes[0].name=host-root-vol,rapidResponse.extraVolumes.volumes[0].hostPath.path=/' \
  --set 'rapidResponse.extraVolumes.mounts[0].name=host-root-vol,rapidResponse.extraVolumes.mounts[0].mountPath=/host'

echo "The rapid response passphrase is ${PASSPHRASE}"
```

Using it in the UI

<SCREENSHOT>

---
[<< Previous: Prerequisites](1-kubernetes-cluster-deployment.md) | [README](../README.md) | [Next: Deploy Sysdig Agent >>](2-deploy-sysdig-agent.md)