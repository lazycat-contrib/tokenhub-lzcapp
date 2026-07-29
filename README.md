# TokenHub for LazyCat

This repository packages [TokenHub](https://github.com/astaxie/TokenHub) as a LazyCat LPK v2 application.

## Runtime

- Upstream image: `ghcr.io/astaxie/tokenhub-backend:0.4.0`
- Frontend: `/` (container port 3000)
- Admin and gateway APIs: `/api/*` and `/v1/*` (container port 8080)
- Persistent data: `/lzcapp/var/data`
- Managed release files: `/lzcapp/var/releases`

The initial administrator username is `admin`. A random password is generated during deployment and is used by LazyCat's passwordless-login injection. The Admin API token and application secret are separate hidden random deployment parameters.

## Build

```bash
mkdir -p dist
lzc-cli project release -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

## Automation

`.github/workflows/lazycat.yml` checks stable TokenHub images, copies the selected `linux/amd64` image to the LazyCat registry, creates a versioned GitHub Release asset, and reconciles both the official and private stores.

The workflow expects these GitHub Secrets:

- `LAZYCAT_TOKEN`
- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID` (optional)
- `PRIVATE_STORE_GROUP_CODES` (optional)
