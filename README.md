# homepage

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.11.0](https://img.shields.io/badge/AppVersion-1.11.0-informational?style=flat-square)

gethomepage.dev dashboard with Kubernetes service discovery and a Traefik IngressRoute

**Homepage:** <https://github.com/Gilk260/helm-homepage>

## Usage

Consumed from git by tag (no Helm repository). Argo CD source:

```yaml
repoURL: https://github.com/Gilk260/helm-homepage
path: .
targetRevision: v0.1.0
```

Dashboard content is declared as maps under `config.services`, `config.bookmarks` and
`config.widgets` and grouped by their `group` field. Maps (not lists) let per-cluster values
files override a single entry, for example only the `href` of one service.

An init container copies the rendered config into a writable `emptyDir` (Homepage needs a
writable `/app/config`), and a config hash annotation restarts the pod on changes.

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Gilk | <Gilk260@gmail.com> |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| config.bookmarks | object | `{}` | Bookmarks as a map; each entry has name, abbr, href and group. |
| config.kubernetes | object | `{"mode":"cluster"}` | kubernetes.yaml content. |
| config.services | object | `{}` | Services as a map; each entry has name, description, icon, href and group. |
| config.settings | object | `{}` | settings.yaml content. |
| config.widgets | object | `{}` | Widgets as a map of widget name to widget config. |
| domain | string | `""` | Hostname for the Traefik IngressRoute. No IngressRoute is rendered when empty. |
| image.repository | string | `"ghcr.io/gethomepage/homepage"` | Homepage image repository. |
| image.tag | string | `"v1.11.0"` | Homepage image tag. |
| initResources | object | `{"limits":{"cpu":"100m","memory":"64Mi"},"requests":{"cpu":"10m","memory":"16Mi"}}` | Resources of the copy-config init container. |
| resources | object | `{"limits":{"cpu":"200m","memory":"128Mi"},"requests":{"cpu":"10m","memory":"64Mi"}}` | Homepage container resources. |
| secret.annotations | object | `{}` | Extra annotations on the ServiceAccount token Secret. |
| service.annotations | object | `{}` | Service annotations. |
| serviceAccount.annotations | object | `{}` | ServiceAccount annotations. |
| serviceAccount.automount | bool | `true` | Mount the ServiceAccount token. |
| serviceAccount.create | bool | `true` | Create the ServiceAccount used for Kubernetes discovery. |
| serviceAccount.name | string | `""` | ServiceAccount name (defaults to the release fullname). |

## License

Apache License 2.0. See [LICENSE](LICENSE).
