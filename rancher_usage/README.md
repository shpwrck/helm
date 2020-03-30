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

Adding the following role to a read-only user will allow them to interface with applications, but not the underlying kubernetes components.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  labels:
    cattle.io/creator: norman
  name: rt-6p65k
  namespace: p-d4b55
rules:
- apiGroups:
  - '*'
  resources:
  - apps
  verbs:
  - create
  - delete
  - get
  - list
  - patch
  - update
  - watch
```

## TODO

- [ ] RBAC App Only User
- [ ] Questions Example
