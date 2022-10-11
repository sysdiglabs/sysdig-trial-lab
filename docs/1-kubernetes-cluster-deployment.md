# Kubernetes Cluster Deployment

## Why a fresh cluster?

We will deploy some workloads that will trigger some alarms and you don't want them to affect your production environment

## Options

There are plenty of options to deploy a k8s cluster, in your laptop, in the cloud, consuming a cloud service... and the list goes on and on. We will be focusing on a couple of examples here but any vanilla k8s cluster should be valid. See https://docs.sysdig.com/en/docs/installation/sysdig-agent/agent-installation/agent-installation-requirements/#orchestration-platforms

* [minikube](1.1-minikube.md)
* [kind](1.2-kind.md)
* [eksctl](1.3-eksctl.md)

---
[<< Previous: Prerequisites](0-prerequisites.md) | [README](../README.md) | [Next: Deploy Sysdig Agent >>](2-deploy-sysdig-agent.md)
