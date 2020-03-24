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
- Configuring a private registry
- Secrets

