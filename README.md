# voidmind Unraid Templates

Unraid Docker templates for [voidmind](https://github.com/voidmind-io) projects, published through
[Community Applications](https://ca.unraid.net).

| App | Image | Template |
|---|---|---|
| [VoidLLM](https://github.com/voidmind-io/voidllm): privacy-first LLM proxy and AI gateway | `ghcr.io/voidmind-io/voidllm` | [`templates/voidllm.xml`](templates/voidllm.xml) |
| [VoidPort](https://voidport.app): expose servers without port forwarding, also behind CGNAT | `ghcr.io/voidmind-io/voidport` | [`templates/voidport.xml`](templates/voidport.xml) |

## Installation

Search for the app name in the **Apps** tab of your Unraid server.

Until the templates are listed in Community Applications you can add them by hand:

```bash
wget -O /boot/config/plugins/dockerMan/templates-user/my-VoidLLM.xml \
  https://raw.githubusercontent.com/voidmind-io/unraid-templates/main/templates/voidllm.xml
```

Replace `voidllm` with `voidport` (and `my-VoidLLM` with `my-VoidPort`) for the other template.
Then go to **Docker → Add Container** and choose *VoidLLM* from the template list.

## VoidLLM notes

- Generate the two keys with `openssl rand -base64 32`. Never change the encryption key after the first start.
- Login credentials and the first `vl_uk_` API key are printed to the container log **once**, on the first start.
- The container runs as `99:100` (nobody:users). If `/data` is not writable:
  `chown -R 99:100 /mnt/user/appdata/voidllm`
- `voidllm.yaml` is optional. Put it into `/mnt/user/appdata/voidllm/config/`, see
  [voidllm.yaml.example](https://github.com/voidmind-io/voidllm/blob/main/voidllm.yaml.example).

## VoidPort notes

- Create a tunnel at [voidport.app/dashboard](https://voidport.app/dashboard) (subscription needed) with the
  local port of your app, e.g. 25565 for Minecraft, and paste its token.
- **Target host**: the LAN IP of the Unraid server for apps with a published port or host networking, or the
  app's container name if both containers share a custom Docker network (set *Network Type* to that network).
- **Local port** is optional and only needed if the app listens on another port than the one saved with the tunnel.
- The container only connects out to the relay and publishes no ports. The log shows the public address,
  e.g. `nbg1.voidport.net:30123`.
- To keep the Let's Encrypt certificate for HTTPS on your own domain across container updates, add a path
  `/home/nonroot/.config/voidport` → `/mnt/user/appdata/voidport` and run `chown 65532:65532 /mnt/user/appdata/voidport`.

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
