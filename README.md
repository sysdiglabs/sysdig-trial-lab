<div align="center">

# Sysdig Trial Lab

<p align="center">
  <img alt="Sysdig Logo" src="https://avatars.githubusercontent.com/u/5068817" height="140" />
  <h3 align="center">Sysdig Trial Lab</h3>
</p>

| :warning: **This is unofficial and unsupported procedure. See the [official documentation](https://docs.sysdig.com/en/docs/sysdig-secure/).** |
| --- |

</div>

The objective of this document is to provide instructions (automated ish) to get the most out of a Sysdig trial, including:

* Deploying a small Kubernetes cluster (minikube, kind or eksctl)
* Deploy the Sysdig Agent
* Deploy a vulnerable application
* Deploy a cryptominer application

Then:

* How to perform a vulnerability scanner against a container image
* How to create runtime policies and rules
* ...

# Environment

In order to have a frictionless environment, a new Kubernetes cluster will be deployed.

# References

* [Sysdig official documentation](https://docs.sysdig.com/en/docs/sysdig-secure)

# Steps

* [0 - Prerequisites](docs/0-prerequisites.md)
* [1 - Kubernetes cluster deployment](docs/1-kubernetes-cluster-deployment.md)
* [1.1 - Minikube](docs/1.1-minikube.md)
* [1.2 - Kind](docs/1.2-kind.md)
* [1.3 - eksctl](docs/1.3-eksctl.md)
* [2 - Deploy Sysdig Agent](docs/2-deploy-sysdig-agent.md)
* [3 - Deploy a vulnerable application](docs/3-deploy-a-vulnerable-application.md)
* [4 - Deploy a cryptominer application](docs/4-deploy-a-cryptominer-application.md)
* [5 - Perform a vulnerability scan](docs/5-perform-a-vulnerability-scan.md)
* [6 - Create runtime policies and rules](docs/6-create-runtime-policies-and-rules.md)
* [99 - Tips and tricks](docs/99-tips-and-tricks.md)