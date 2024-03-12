
# Workload Protection (DART-2) - Image scanning
> Date: 2024-02-13
> Tags: #Sue #Incubator #AquaSecurity #Image_scanning 

## Key Concepts
- Scanning container images in repositories

## Detailed Notes
- First the registry need to be add in the `Workload Protection` module. After the registry is added, the images that need to be scanned can be added in the `Images` section
- The first image scan results in two critical CVE's and three forms of malware.
- It is also possible to have AquaSecurity automatically scan the images based on time, every day, week or month at certain times. This can be configured through `Administration` -> `Integrations` -> `The regisrty` -> `Registry Configuration`
- It is also possible to use additional scanners, these can be deployed through `Administration` -> `Scanners` this creates a command to run the scanner on a cluster, example command: `docker run -d  registry.aquasec.com/scanner:2401.3.21 daemon --token 6c600ae10dd93b8e82e5d71f81eccff1b394f049 --host https://b311a5bf11-d.cloud.aquasec.com`

## Diagrams / Images
- First image scan results:![[image_scan.png]]
- Result of automatic scan: ![[auto_scan.png]]

## References
- 


kubectl create secret generic aqua-scanner \
  --from-literal=AQUA_TOKEN=46ca8f3c148ccf31c066e4759c432a70bfdb555 \
  --from-literal=AQUA_SERVER=https://b311a5bf11-d.cloud.aquasec.com \
