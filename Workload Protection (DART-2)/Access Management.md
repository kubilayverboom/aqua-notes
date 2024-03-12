
# Workload Protection (DART-2) - Access Management
> Date: 2024-02-15
> Tags: #Sue #AquaSecurity #Access_Management

## Key Concepts
- Using RBAC to scope access to the portal

## Detailed Notes
- In the `Account Management` module `User Management` -> `Permisions Sets` new sets of permisions can be made for users:
	
| Permission name    | Access        |
|:------------------ |:------------- |
| Assurance Policies | View          |
| Build Pipelines    | Not Permitted |
| Code Repositories  | View          |
| Dependencies       | Not Permitted |
| Integrations       | View          |
| Release Artifacts  | Not Permitted |
| Risks              | View          |
| Suppression Rules  | Edit          |
| Tool Chains        | Not Permitted |
- In the `Application Scope` a new scope can be made, the scope is limited to:
	- The aqua-dart cluster & runtime-policy ns
	- The Hydro SS repository
## Diagrams / Images
- A new role is created which add the limited application scope and permisions sets: ![[access_management.png]]
- Loggin in with the restricted user: ![[restricted_user.png]]
- The modules the user has acces to: ![[restricted_module.png]]

## References
- 
