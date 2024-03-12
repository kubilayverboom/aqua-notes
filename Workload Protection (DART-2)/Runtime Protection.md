
# Workload Protection (DART-2) - Runtime Protection
> Date: 2024-02-14
> Tags: #Sue #AquaSecurity #Runtime_Protection

## Key Concepts
- Going through config of Enforces by using the classic mode set in `Settings` - > `Runtime Protection`
- Looking at the different types of protection

## Detailed Notes
- vShield can be employed to mitigate access to vulnerable resources within container images. To view available vShields, select an image from the scanner, and under `Vulnerabilities`, enable vShield for vulnerabilities with an "active" vShield button.
- With the vShield active, the deployment just runs as normal.
- Using the custom runtime policy, when trying to deploy with an unregistered image, this get's denied and the following output is presented:
	   `Error from server: admission webhook "imageassurance.aquasec.com" denied the request: [Aqua Security] Image is unregistered with Aqua server.`
- Trying to run an non-compliant image results in this error:
	  `Error from server: error when creating "runtime.yml": admission webhook "imageassurance.aquasec.com" denied the request: [Aqua Security] Image is marked as non-compliant.`

## Diagrams / Images
- Under `Security Reports` -> `Vulnerabilities` -> `All Vulnerabilities` an overview of all active vShields, either in enforce or audit mode can be seen: ![[active_vschields.png]]
- Using `wget` to tho test the drift detection errors in the container not being allowed to execute the separately installed `wget`. An audit message can be found in `Security Reports` -> `Audit`: ![[drift_detection.png]]
- Sidecar with the Pod- and Micro enforcer: ![[pod_micro_enforcer.png]]


## References:

- 
  ```shell
  helm upgrade --install --create-namespace --namespace aqua aqua-kube-enforcer aqua-helm/kube-enforcer --set global.gateway.address=b311a5bf11-d-gw.cloud.aquasec.com,global.gateway.port=443,certsSecret.autoGenerate=true,global.platform=k8s,global.enforcer.enabled=true,aquaSecret.kubeEnforcerToken=acfcf3bd-7202-42c6-9f63-096cfdb3d31b,image.tag=2022.4,enforcer.enforcerToken=b4014bd7-5ece-4477-9359-af9be04a2cca,enforcer.image.tag=2022.4,serviceAccount.create=true,clusterName=aqua-darts,global.imageCredentials.create=true,global.imageCredentials.repositoryUriPrefix=registry.aquasec.com,global.imageCredentials.registry=registry.aquasec.com,global.imageCredentials.username=kubilay.verboom@sue.nl,global.imageCredentials.password=T@uvSrJ6LJA8e28v,enforcer.expressMode=true
```
