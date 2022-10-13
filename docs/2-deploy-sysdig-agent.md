* lots of options - script, helm,...
* helm is the easiest

```
export SYSDIG_ACCESS_KEY="xxx"
export SAAS_REGION="eu1"
export COLLECTOR_ENDPOINT="ingest-eu1.app.sysdig.com"
export COLLECTOR_PORT="6443"
export API_ENDPOINT="eu1.app.sysdig.com"

helm repo list | grep -q sysdig || helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig sysdig/sysdig-deploy \
  --namespace sysdig-agent \
  --create-namespace \
  --set global.sysdig.accessKey=${SYSDIG_ACCESS_KEY} \
  --set global.sysdig.region=${SAAS_REGION} \
  --set global.clusterConfig.name=${K8S_CLUSTER_NAME} \
  --set nodeAnalyzer.secure.vulnerabilityManagement.newEngineOnly=true \
  --set nodeAnalyzer.nodeAnalyzer.apiEndpoint=${API_ENDPOINT} \
  --set nodeAnalyzer.nodeAnalyzer.runtimeScanner.deploy=true \
  --set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.eveEnabled=true \
  --set nodeAnalyzer.nodeAnalyzer.runtimeScanner.eveConnector.deploy=true \
  --set global.kspm.deploy=true \
  --set agent.sysdig.settings.collector=${COLLECTOR_ENDPOINT} \
  --set agent.sysdig.settings.collector_port=${COLLECTOR_PORT} \
  --set agent.sysdig.settings.drift_killer.enabled=true \
  --set agent.sysdig.settings.tags='dept:tmm' \
  --set agent.slim.enabled=true \
  --set agent.psp.create=false

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

---
[<< Previous: Kubernetes cluster deployment](1-kubernetes-cluster-deployment.md) | [README](../README.md) | [Next: Deploy a vulnerable application](3-deploy-a-vulnerable-application.md)