# Headers component theme

The _Headers_ component theme for [Cecil](https://cecil.app) provides support of `_headers` file generation.

After installation and without any configuration, this component theme generates a [`_headers`](./layouts/_default/page.headers.twig) file containing default HTTP headers (security and cache) and the HTTP headers defined in the [`server.headers` configuration](https://cecil.app/documentation/configuration/#server-headers).

Services that support the `_headers` file:

- [Netlify](https://docs.netlify.com/manage/routing/headers/)
- [statichost](https://www.statichost.eu/docs/custom-headers/)
- [Cloudflare Pages](https://developers.cloudflare.com/pages/configuration/headers/)

> [!NOTE]
> The [_Netlify_ component theme](https://github.com/Cecilapp/theme-netlify) already generates a `_headers` file: don't use both themes together.

## Installation

```bash
composer require cecil/theme-headers
```

> Or [download the latest archive](https://github.com/Cecilapp/theme-headers/releases/latest/) and uncompress its content in `themes/headers`.

## Usage

Add `headers` in the `theme` section of your site configuration:

```yaml
theme:
  - headers
```

The `_headers` file is generated at the root of the output directory (`_site/` by default).

### Add headers

```yaml
server:
  headers:
    - path: <path> # Relative path, prefixed with a slash. Support "*" wildcard.
      headers:
        - key: <key>
          value: "<value>"
```

Documentation: <https://cecil.app/documentation/configuration/#server-headers>

Your headers are added after the default headers of the theme (they are also applied by the local preview server `cecil serve`).

#### Default headers

The theme provides the following [default headers](./config.yml):

| Path | Headers |
| --- | --- |
| `/*` | `X-Frame-Options`, `X-Content-Type-Options`, `Strict-Transport-Security` |
| `/favicon*`, `/logo*`, `/icon*`, `/assets/*`, `/images/*`, `/videos/*`, `/styles/*`, `/css/*`, `/*.css`, `/fonts/*` | `Cache-Control: public, max-age=31536000` (1 year) |
| `/javascript/*`, `/js/*`, `/*.js` | `Cache-Control: private, max-age=31536000` (1 year) |
| `/serviceworker.js`, `/manifest.webmanifest` | `Cache-Control: no-cache` |
| `/admin/*` | `Cache-Control: no-cache, no-store, must-revalidate`, permissive `Content-Security-Policy` |

> [!IMPORTANT]
> Files with a long cache lifetime should have a fingerprint in their name (see [`assets.fingerprint`](https://cecil.app/documentation/configuration/#assets)), otherwise visitors may not receive their updates.

To replace the default headers, copy them from the theme [`config.yml`](./config.yml) into the `headers.default` section of your site configuration, then edit them. To disable them:

```yaml
headers:
  default: false
```

> When a path matches several rules, the headers of all matching rules are applied.

## License

_Headers_ is a free software distributed under the terms of the MIT license.

© [Arnaud Ligny](https://arnaudligny.fr)
