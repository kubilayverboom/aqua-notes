
# Workload Protection (DART-2) - CICD Scanning
> Date: 2024-02-14
> Tags: #Sue #AquaSecurity #CI/CD 

## Key Concepts
- Image scanning in an existing pipeline

## Detailed Notes
- In the Aqua SaaS portal, in the `Workload Protection` module, by navigating to `Administration` -> `Scanner` a token can be generated for the scanner.
- For the first part, using the Aqua Scanner Container, the image was scanned that's being made in the CI/CD in GitLab, the following step in the pipeline is used:

```yml
	image: docker:latest
	
	variables:
	  DOCKER_DRIVER: overlay2
	  DOCKER_TLS_CERTDIR: ""
	
	services:
	  - docker:dind
	
	stages:
	  - build
	  - scan
	
	customer_image_build:
	  stage: build
	  script:
	    - echo "This represents your build of the Docker image"
	    - docker build . --file Dockerfile --tag my-demo-image:$CI_COMMIT_SHA
	    - docker tag my-demo-image:$CI_COMMIT_SHA docker.io/kubilayverboom/my-demo-image:$CI_COMMIT_SHA
	    - echo "$DOCKERHUB_PASSWORD" | docker login docker.io -u $DOCKERHUB_USERNAME --password-stdin
	    - docker push docker.io/kubilayverboom/my-demo-image:$CI_COMMIT_SHA
	
	scanner:
	  stage: scan
	  script:
	    - echo "$AQUASEC_PASSWORD" | docker login registry.aquasec.com -u $AQUASEC_USERNAME --password-stdin
	    - docker run --rm -v /tmp:/tmp -v /var/run/docker.sock:/var/run/docker.sock registry.aquasec.com/scanner:2401.3.21 scan --registry "Docker Hub" kubilayverboom/my-demo-image:$CI_COMMIT_SHA --host https://b311a5bf11-d.cloud.aquasec.com/ --token $AQUASEC_TOKEN  --register --show-negligible --htmlfile /tmp/out.html --jsonfile /tmp/out.json > /dev/null
	    - cp /tmp/out.html /tmp/out.json .
	  artifacts:
	    paths:
	    - out.json
	    - out.html
```


## Diagrams / Images
- Pipeline failing because of assurance policy: ![[failed_cicd.png]]
- Image being added to the console: ![[image_in_console.png]]

## References
- [Scanner Commands](https://docs.aquasec.com/saas/workload-protection/aqua-scanner/aqua-scanner-command-line/examples-of-scanner-commands/)
- [CI/CD Integrations](https://docs.aquasec.com/saas/workload-protection/integrations/cicd-integrations/)
