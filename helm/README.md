# Creating Helm chart

Let's use helm cli in order to create a vanilla Helm chart directory for a given chart name which we'll choose to match the name of the fictive application, `my-app` (in future maybe consider using word `chart` in the name, like `my-app-chart`):

```
$ helm create my-app
Creating my-app
```
This command creates a Helm chart boilerplate in a directory `my-app`.

# Linting Helm chart

```
$ helm lint ./my-app/
==> Linting ./my-app/
[INFO] Chart.yaml: icon is recommended

1 chart(s) linted, 0 chart(s) failed
```

