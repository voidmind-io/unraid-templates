# voidmind Unraid Templates

Unraid Docker templates for [voidmind](https://github.com/voidmind-io) projects, published through
[Community Applications](https://ca.unraid.net).

| App | Image | Template |
|---|---|---|
| [VoidLLM](https://github.com/voidmind-io/voidllm): privacy-first LLM proxy and AI gateway | `ghcr.io/voidmind-io/voidllm` | [`templates/voidllm.xml`](templates/voidllm.xml) |

## Installation

Search for the app name in the **Apps** tab of your Unraid server.

Until the templates are listed in Community Applications you can add them by hand:

```bash
wget -O /boot/config/plugins/dockerMan/templates-user/my-VoidLLM.xml \
  https://raw.githubusercontent.com/voidmind-io/unraid-templates/main/templates/voidllm.xml
```

Then go to **Docker → Add Container** and choose *VoidLLM* from the template list.

## VoidLLM notes

- Generate the two keys with `openssl rand -base64 32`. Never change the encryption key after the first start.
- Login credentials and the first `vl_uk_` API key are printed to the container log **once**, on the first start.
- The container runs as `99:100` (nobody:users). If `/data` is not writable:
  `chown -R 99:100 /mnt/user/appdata/voidllm`
- `voidllm.yaml` is optional. Put it into `/mnt/user/appdata/voidllm/config/`, see
  [voidllm.yaml.example](https://github.com/voidmind-io/voidllm/blob/main/voidllm.yaml.example).

## Repository layout

```
ca_profile.xml        maintainer profile for Community Applications
templates/*.xml       one Unraid template per app
icons/*.png           app icons referenced by the templates
```

## Adding a template

1. Add `templates/<app>.xml` and `icons/<app>.png`.
2. Point `<TemplateURL>` and `<Icon>` at the raw GitHub URLs on `main`.
3. Add a row to the table above.

## License

The templates in this repository are MIT licensed. The applications they install have their own licenses.
