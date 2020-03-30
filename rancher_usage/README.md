# Rancher Usage

## Adding Catalogs

## Chart Lifecycle

## Rancher Additions

- `app-readme.md` Adds descriptive text to the UI
- `questions.yaml` Adds self-guided support in the UI
  -  Validation
  -  Conditionals
  -  Rancher Supported Versions

## Chart/Catalog RBAC

### Chart/Catalog based roles

Catalogs can be scoped to all three levels [`global`,`cluster`, `project`] which can make rbac permutations a bit complex.

- To allow interacting with globally scoped catalogs use `Manage Catalogs` or `Use Catalog Templates`
- To allow interacting with cluster scoped catalogs use `Manage Cluster Catalogs` or `View Cluster Catalogs`
- To allow interacting with project scoped catalogs use `Manage Project Catalogs` or `View Project Catalogs`

## TODO

- [ ] RBAC App Only User
- [ ] Questions Example
