
# Workload Protection (DART-2) - Response Policies
> Date: 2024-02-16
> Tags: #Sue #AquaSecurity #Response_Policies

## Key Concepts
- Using response policies when there are important events.

## Detailed Notes
- In the `Aqua Hub` module a new `Response Policy` can be created. Two new policies will be created, one will trigger on a scan result and the other on runtime events.
	- The scan results will trigger if an image that is being scanned is non-compliant.

## Diagrams / Images
- To trigger the first response policy, the wordpress image is used, an snippet of the JSON output:
```json
"previous_digest": "sha256:29cf1d10dc09b90d6fd82193703ca780374a11389ac012c0d7da9f11f7ce07c4",
  "registry": "Hydrogic SS",
  "resourceTypeKey": "image",
  "response_policy_name": "Critical scann results",
  "scan_id": 47,
  "scan_options": {
    "dockerless": true,
    "enable_diff_ids": true,
    "enable_fast_scanning": true,
    "is_trivy_enabled": true,
    "manual_pull_fallback": true,
    "memoryThrottling": true,
    "scan_executables": true,
    "scan_files": true,
    "scan_malware": true,
    "scan_sensitive_data": true,
    "scan_timeout": 3600000000000,
    "suggest_os_upgrade": true,
    "telemetry_enabled": true,
    "use_cvss3": true
  },
  "scan_result_unique_properties": {
    "digest": "sha256:29cf1d10dc09b90d6fd82193703ca780374a11389ac012c0d7da9f11f7ce07c4",
    "image": "wordpress:latest",
    "registry": "Hydrogic SS"
  },
```
	  

## References
- [Response Policies](https://docs.aquasec.com/v2022.4/platform/response-policies/response-policies/)
