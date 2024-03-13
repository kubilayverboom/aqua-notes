
# AquaSecurity - Workload Protection (DART-2)
> Date: 2024-03-12
> Tags: #AquaSecurity #DART-2 #Workload_Protection

## I. Image Registry
The Workload Protection module scan images in a registry for vulnerabilities, it can also scan active images that are being used.

Integrating an image registry is easy, this can be done through **Administration** -> **Integrations**.
![added_registry](./assets/added_registry.png)

With the registry integrated, images in that registry can be scanned. This can be through **Images & Functions** -> **Images** -> **Add Images**. For the assignment, the `jerbi/eicar:latest` image will be scanned. The initial scan will show that the image has two critical CVEs and three forms of malware.

![Image_scan](./assets/image_scan_result.png)

Next to being able to add and scan images manually, it is possible to automate this task. This can be done through **Administration** -> **Integrations** -> **${registry_name}** -> **Registry Configurations**.

![all_images](./assets/all_images.png)

### Additional Scanner
Next to being able to scan an image registry, it is also possible to deploy a scanner in a K8S cluster. This way, images used in production are being scanned. The deployment can be done through **Administration** -> **Scanners**.

The command that is needed to deploy the scanner is shown:
```bash
docker run -d  registry.aquasec.com/scanner:2402.8.22 daemon --token <token> --host https://7b02ff4f90.cloud.aquasec.com
```

When the container is deployed successfully it can be listed:
![scanner_container](./assets/scanner_container.png)

After the scanner is deployed, under **Administration** -> **Integrations** the Hydrogic scanner can connected to the Hydrogic registry for image scanning.

![scanner_dashboard](./assets/scanner_dashboard.png)


## II. Assurance Policies


## III. Main Topic 3
 

## Summary
- [Summarize the main points of the outline]

## Additional Resources
- [Links to relevant resources]