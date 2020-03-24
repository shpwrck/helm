# Getting Started

## Installing Helm

### Most Recent

Executing `install_helm.sh` will install the latest version of helm.

### Specific Version

If a specific release is desired, install from binary.

1. Download target release: https://github.com/helm/helm/releases
1. Unpack it `tar -zxvf ...`
1. Relocate it `mv source destination`

## Terminology

- Chart: The template from which your application will be generated.
- Repository/Catalog: A collection of helm charts ( e.g. https://git.rancher.io/charts )
- Release: An instance of a template; the specific name/namespace/cluster configuration.
- Chart Museum: A registry for charts. Similar to a docker registry in which you push/pull charts.

## Helm Basic Commands

### Release Lifecycle

- `helm install`
- `helm status` 
- `helm upgrade`
- `helm rollback`
- `helm uninstall`

### Chart Lifecycle

- `helm repo add/list/update/remove`
- `helm create`
- `helm package`

## Using Values

### Using command line options

Values can be modified at installation using the `--set` flag. This flag allows for the following options:

- Multiple values separated by `,` as in `--set key1=value1,key2=value2`
- Nesting values using the `.` operator as in `--set parent.child=childvalue`
- Arrays using `[` and `]` as in `--set keys={value1,value2,value3}`
- Indices using `[#]` as in `--set index[1].key=value`
- and character escaping using `\` as in `--set keywithtwovalues=value1\,value2`

### Using values.yml

Values can be represented and stored alongside charts as a properly formatted yaml file.
All of the options above would result in the following value.yml:

```
key1: value1
key2: value2
parent:
  child: childvalue
keys:
- value1
- value2
- value3
index:
- 
- key: value
keywithtwovalues: "value1,value2"
```

**Note** Using the cli `--set` option in conjunction with a `values.yml` will overide configuration in the file with the cli options.

## Creating a Repository



## Creating a Chart

## Further Topics

- Post Rendering
- Chart Hooks
- Chart Tests
- Helm Provenance and Integrity
- Library Charts
- Registries

