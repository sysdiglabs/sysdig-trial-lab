* Why are we testing ML Policy

The ML Team, with the help of the Threat Research Team, have built a cluster environment in which we run some sample miners. <br/>
These miners are run using docker images, which are publicly available on Dockerhub and Github: <br/>
https://hub.docker.com/r/metal3d/xmrig

* Explain machine learning vs matching

The data models are unique, so data is actually merged across regions, after being anonymized. <br/>
References to the original customer are dropped along with sensitive data before fingerprints are moved to the ML sandbox where we train models. <br/>
<br/>
The algorithm is using data collected from across regions (so far only us-east-1, but we are not limited to it for future collection). <br/>
That being said, we don't keep any information tracing back to the customer because all sensitive fields are anonymised.

* Confidence levels

Based on these algorithms, Sysdig Secure provides a confidence rating in % to see if it's a cryptominer or not:

<img width="1294" alt="Screenshot 2022-10-20 at 10 03 16" src="https://user-images.githubusercontent.com/109959738/196905537-32051a01-6d57-40ad-b1f0-24970ebdcdcf.png">



* How to enable it

In the case you wished to perform a live demo, you can mimic the procedure that was used to create the offline environment and install it in your own machine/EC2 instance etc.. <br/>
To be specific, we set up a minikube cluster running on an EC2 instance <br/>

<br/>
First, you’ll need a Kubernetes Cluster, run with minikube or an analogous tool. <br/>
Then, install the latest version of the sysdig-agent which points at the collector of the desired account.

### ENABLE PROFILING: 

To do so, go to the settings page on Sysdig. <br/>
You’ll find a toggle on the bottom, under the Sysdig Labs section, since it’s currently available in tech preview. <br/>
<br/>
You will then need to create a deployment in which to run the ```<miner_image>``` , which is inserted in the deployment template below. <br/>
Make sure to edit the the image name and the resources to allocate to the container. <br/>
<br/>
We suggest the default memory resources, but they can be modified based on need. <br/>
Bear in mind that too high resources may overflow your cluster and may cause the agent to drop fingerprints. <br/> 
Too little resources will not allow for enough mining jobs to be spawned and therefore there will be less detections.

* Test it

Create a Network Namespace for the miner deployment
```
apiVersion: v1
kind: Namespace
metadata:
  creationTimestamp: null
  name: miner-test
spec: {}
status: {}
```

Create the miner deployment within the miner-test namespace
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: miner
  name: miner
  namespace: miner-test
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: miner
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: miner
    spec:
      containers:
      - env:
        - name: POOL_URL
          value: pool.minexmr.com
        image: metal3d/xmrig:latest
        imagePullPolicy: Always
        name: xmrig
        resources:
          limits:
            cpu: 0.5
            memory: 4Gi
          requests:
            cpu: 0.25
            memory: 2Gi
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
 ```
 
We should use the above deployment when we have greater confidence in the ML policy feature. <br/>
For now, we were only able to generate successful detections via the Sysdig Threat Generator: <br/>
https://github.com/sysdig/sysdig-threat-generator/blob/main/kubernetes/Sysdig-Threat-Generator.yaml
