# Headers component theme

The _Headers_ component theme for [Cecil](https://cecil.app) provides support of `_headers` file generation.

After installation and without any configuration, this component theme generate a [`_headers`](./layouts/_default/page.headers.twig) file containing HTTP headers created by Cecil (generated from [`headers' configuration`](https://cecil.app/documentation/configuration/#headers))

Services that support the `_headers` file:

- [Netlify](https://docs.netlify.com/manage/routing/headers/)
- [statichost](https://www.statichost.eu/docs/custom-headers/)
- [Cloudflare Pages](https://developers.cloudflare.com/pages/configuration/headers/)

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

### Add headers

```yaml
headers:
  - path: <path> # Relative path, prefixed with a slash. Support "*" wildcard.
    headers:
      - key: <key>
        value: "<value>"
```

Document: <https://cecil.app/documentation/configuration/#headers>.
