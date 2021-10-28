# Matomo Chart

Matomo is an open source alternative to Google Analytics. (Ported from: https://gitlab.com/ideaplexus/helm/matomo/-/tree/master/)

## Install

```sh
helm install matomo . --namespace matomo --create-namespace
```

## Upgrade

```sh
export REDIS_PASSWORD=$(kubectl get secret --namespace "matomo" matomo-redis -o jsonpath="{.data.redis-password}" | base64 --decode)

helm upgrade matomo . --namespace matomo --set redis.auth.password=$REDIS_PASSWORD 
```

## Parameters

Most relevant parameters, if you need an advanced configuration, take a look into the `values.yaml`.

| Parameter                            | Description                                               | Default                                  |
| :----------------------------------- | :-------------------------------------------------------- | :--------------------------------------- |
| `replicaCount`                       | How many instances of Matomo should run in parallel       | `1`                                      |
| `image.tag`                          | Override the version tag for the Matomo docker image      | `""` (Using chart appVersion)            |
| `ingress.enabled`                    | If `true`, an Ingress is created                          | `false`                                  |
| `ingress.rules`                      | List of Ingress Ingress rule                              | see below                                |
| `ingress.rules[0].host`              | Host for the Ingress rule                                 | `{{ .Release.Name }}.matomo.example.com` |
| `ingress.rules[0].paths`             | Paths for the Ingress rule                                | see below                                |
| `ingress.rules[0].paths[0].path`     | Path for the Ingress rule                                 | `/`                                      |
| `ingress.rules[0].paths[0].pathType` | Path Type for the Ingress rule                            | `Prefix`                                 |
| `ingress.servicePort`                | The Service port targeted by the Ingress                  | `http`                                   |
| `ingress.annotations`                | Ingress annotations                                       | `{}`                                     |
| `ingress.ingressClassName`           | The name of the Ingress Class associated with the ingress | `""`                                     |
| `ingress.labels`                     | Additional Ingress labels                                 | `{}`                                     |
| `ingress.tls`                        | TLS configuration                                         | see below                                |
| `ingress.tls[0].hosts`               | List of TLS hosts                                         | `[matomo.example.com]`                   |
| `ingress.tls[0].secretName`          | Name of the TLS secret                                    | `""`                                     |
| `matomo.host`                        | Host of the Matomo installation                           | `chart-example.local`                    |
| `matomo.username`                    | Superusers name                                           | `admin`                                  |
| `matomo.password`                    | Superusers password                                       | `My$uper$ecretPassword123#`              |
| `matomo.email`                       | Superusers email address                                  | `admin@chart-example.local`              |
| `matomo.website_host`                | Host of the tracked website                               | `https://tracked-website.local`          |
| `matomo.website_name`                | Name of the tracked website                               | `Tracked Website`                        |
| `matomo.env`                         | Additional Environment variables, e.g. to configure SMTP  | `{}`                                     |



