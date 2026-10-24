# xray-geodata

Minimal, curated `geosite.dat` and `geoip.dat` for [Xray-core](https://github.com/XTLS/Xray-core),
built automatically from pinned upstream sources.

This repository contains **build artifacts, this README and license notices** —
no source lists, no templates, no credentials. Sources are described in
`manifest.json` and in [LICENSE-NOTICES.md](LICENSE-NOTICES.md).

## Artifacts

| File | Description |
|---|---|
| `geosite.dat` | 34 domain categories (see `manifest.json`) |
| `geoip.dat` | 10 IP categories (see `manifest.json`) |
| `manifest.json` | version, build time, source commits/sha256, per-category counts, artifact sha256/size, `xray run -test` result |
| `*.sha256` | per-file checksums |
| `SHA256SUMS` | all checksums in one file |
| `LICENSE-NOTICES.md` | upstream attribution and licenses |
| `LICENSE-GPL-3.0.txt` | full GPL-3.0 text (derived geoip/ads data) |

Stable raw URLs (updated in place on every release, orphan `release` branch):

```
https://raw.githubusercontent.com/evgenyzh/xray-geodata/release/geosite.dat
https://raw.githubusercontent.com/evgenyzh/xray-geodata/release/geoip.dat
https://raw.githubusercontent.com/evgenyzh/xray-geodata/release/manifest.json
```

Immutable, versioned downloads are attached to
[releases](https://github.com/evgenyzh/xray-geodata/releases).

## Verify a download

```bash
curl -fSLO https://raw.githubusercontent.com/evgenyzh/xray-geodata/release/geosite.dat
curl -fSLO https://raw.githubusercontent.com/evgenyzh/xray-geodata/release/geoip.dat
curl -fSLO https://raw.githubusercontent.com/evgenyzh/xray-geodata/release/SHA256SUMS
sha256sum -c SHA256SUMS
```

> `raw.githubusercontent.com` is CDN-cached for up to 5 minutes. For a few
> minutes after a new build, the `release` branch files can be a mix of old and
> new. Retry, or use the immutable assets attached to the
> [release](https://github.com/evgenyzh/xray-geodata/releases) for strict
> verification.

Check the version, source pins and category counts:

```bash
curl -fSLO https://raw.githubusercontent.com/evgenyzh/xray-geodata/release/manifest.json
python3 -m json.tool manifest.json | head -40
```

Smoke-test with Xray (all categories must resolve):

```bash
XRAY_LOCATION_ASSET=. xray run -test -c /path/to/config.json
```

## Usage

```json
{
  "routing": {
    "rules": [
      {
        "type": "field",
        "domain": ["geosite:ru-blocked", "geosite:category-ads-all"],
        "ip": ["geoip:ru", "geoip:private"],
        "outboundTag": "direct"
      }
    ]
  }
}
```

Category names are stable across releases. `manifest.json` lists every category
and its rule count; an unknown category makes `xray` fail with
`code not found in geosite/geoip`.

## Builds

- Daily at 04:00 UTC, on demand, and on changes to the private build inputs.
- Built with Go 1.26 from a pinned
  [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
  commit; geosite is filtered to the needed categories, geoip is filtered from
  [runetfreedom/russia-blocked-geoip](https://github.com/runetfreedom/russia-blocked-geoip).
- `ru-blocked` is curated: community antifilter list + media + libraries +
  trackers + extra sites, minus a small deny list (gambling).
- Every build is checked with `xray run -test` against all categories before
  publication.

## License

Artifacts are compiled data derived from MIT and GPL-3.0 upstream datasets.
See [LICENSE-NOTICES.md](LICENSE-NOTICES.md) and
[LICENSE-GPL-3.0.txt](LICENSE-GPL-3.0.txt). No warranty; categorization is
approximate and provided as-is.
