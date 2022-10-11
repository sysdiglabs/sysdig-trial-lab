# Prerequisites

## Sysdig account

For getting the most of this lab, a Sysdig account is required.

A 30 days free trial account is available and perfectly valid. It takes literally 5 minutes to register and it doesn't require any credit card.

The process is really simple:

* Visit the [Sysdig trial site](https://sysdig.com/company/start-free/)
* Select all the features you want to try (all of them!)
* Add your personal details, including the cloud region closest to you
<SCREENSHOT>

That's it!

You will receive an email explaining how to access the Sysdig portal and configure a password:

<SCREENHOST>

## Sysdig access key

The Sysdig backend is a multitenant environment where every user/team has a unique access key to identify himself against it. The unique access key tied to your account can be observed in the agent installation URL such as `https://eu1.app.sysdig.com/secure/#/settings/agentInstallation` where the host `eu1.app.sysdig.com` will be different depending on your cloud region.

[CLOUD REGIONS](https://docs.sysdig.com/en/docs/administration/saas-regions-and-ip-ranges/#saas-regions-and-ip-ranges)

It should look like a bunch of numbers and dashed such as `381e41ea-494f-11ed-b878-0242ac120002`

It is important to keep in mind this access key identifies your Sysdig account and it should be treated as a password, save it somewhere safe (password manager) and don't share it!

## Network connectivity

It is required to be able to connect to the Sysdig backend servers to report metrics & data. The K8s clusters where the agent will be deployed must be able to reach the Sysdig Collector addresses.

Also, the `sysdig-cli-scanner` tool that performs container image scanning requires access to the Sysdig API to gather the vulnerability databases and to push the scanning results.

[CLOUD REGIONS](https://docs.sysdig.com/en/docs/administration/saas-regions-and-ip-ranges/#saas-regions-and-ip-ranges)

---
[<< Back to README](../README.md) | [Next: Kubernetes cluster deployment >>](1-kubernetes-cluster-deployment.md)