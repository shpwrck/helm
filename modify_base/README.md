# Modify Base

## Built-in Objects

- Release
  - .Name
  - .Namespace
  - .IsUpgrade
  - .IsInstall
  - .Revision
  - .Service
- Values (.etc as defined in Values.yamlG)
- Chart (.etc as defined in Chart.yaml)
- Files (.etc many ways of getting non-special files)
- Capabilities (Kubernetes related capabilities)
- Template
  - .Name
  - .BasePath


## Values Functions

- Sprig Library -> https://masterminds.github.io/sprig/
- `include` Makes the template libraries extensible
- `required` Makes a chart fail/succeed at rendering given a value
- `tpl` Allows the parsing of templates that are stored inside value definition.

## Flow Control

- `if/else`

```
{{ if CONDITION }}
# Do Something
{{ else if OTHER CONDITION }}
# Do Something
{{ else }}
# Do something by default
{{ end }}
```

- `with` 

```
{{ with .Values.subscope }}
  key: {{ .subscopevalue #Restricted to subscope }}
{{ end }}
```

- `range`

```
{{ range .Values.list }}
- {{ . #list items }}
{{ end }}
```

```
{{ range tuple "value1" "value2" "value3" }}
- {{ . }}
{{ end }}
```

- `define` Used inside of a named template to be used with the template label.
- `template` Used to apply a `defined` template.
- `block` Define and execute a template in place

## Misc

- `{{-` or `-}}` whitespace chomp before and after
- Typecasting use `{{ int $value }}` or `{{ $value | quote }}`
- Inline variables `{{ $variable := $value }}`
- `{{ $.xxx }}` represents the root scope. (Useful within `range`/`with`)

## Special Considerations

### Nesting Charts

You can add a `requirements.yaml` to a given chart to establish chart dependency.
The example below comes from [here](https://github.com/helm/charts/tree/master/stable/prometheus-operator)
```
dependencies:

  - name: kube-state-metrics
    version: "2.6.*"
    repository: https://kubernetes-charts.storage.googleapis.com/
    condition: kubeStateMetrics.enabled

  - name: prometheus-node-exporter
    version: "1.9.*"
    repository: https://kubernetes-charts.storage.googleapis.com/
    condition: nodeExporter.enabled

  - name: grafana
    version: "5.0.*"
    repository: https://kubernetes-charts.storage.googleapis.com/
    condition: grafana.enabled
```

The components from `kube-state-metrics`, `prometheus-node-exporter`, and `grafana` are required in order for the `prometheus-operator` chart to install.

### Server side validation

In Helm 3, json schema was introduced. [link](https://github.com/helm/community/blob/master/helm-v3/001-charts.md#schematized-values-files)

Prior to Helm 3, the solution would look something like this:

```
# something.tpl
{{- define "actionValidate" -}}
  {{ $action := .Values.actions }}
  {{- if or (eq $action "true") (eq $action "alsotrue") -}}
    true
  {{- end -}}
{{- end -}}

```
```
# manifest.yaml
{{ include "actionValidate" .  | required "Action value is incorrect. The valid values are 'true' and 'alsotrue'." }}
```


### Configuring a private registry

```
imageCredentials:
  registry: quay.io
  username: someone
  password: sillyness
```

```
{{- define "imagePullSecret" }}
{{- printf "{\"auths\": {\"%s\": {\"auth\": \"%s\"}}}" .Values.imageCredentials.registry (printf "%s:%s" .Values.imageCredentials.username .Values.imageCredentials.password | b64enc) | b64enc }}
{{- end }}
```

```
apiVersion: v1
kind: Secret
metadata:
  name: myregistrykey
type: kubernetes.io/dockerconfigjson
data:
  .dockerconfigjson: {{ template "imagePullSecret" . }}
```
