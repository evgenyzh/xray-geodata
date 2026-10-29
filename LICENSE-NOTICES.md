# License and attribution notices

These notices apply to the generated geodata artifacts in this directory
(`geosite.dat`, `geoip.dat`, `manifest.json`, checksums) and to the public
artifact repository `evgenyzh/xray-geodata`.

The artifacts are compiled data. They are **not** a copy of any project's
source tree, but they are derived from the upstream datasets listed below.

## 1. v2fly/domain-list-community — MIT

- Source: https://github.com/v2fly/domain-list-community
- Pinned commit: `9cad4889b6f1c51bd84cb8a0d95dbc1a992251a4`
- Used for: the geosite builder (`main.go`, `internal/dlc`) and the list
  sources that make up most `geosite.dat` categories, including
  `data/category-media-ru-blocked`.
- License: MIT

```
MIT License

Copyright (c) 2018-2019 V2Ray

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

`geosite.dat` uses the protobuf schema from
[v2fly/v2ray-core](https://github.com/v2fly/v2ray-core)
(`app/router/routercommon`), also MIT.

## 2. runetfreedom/russia-blocked-geosite — GPL-3.0

- Source: https://github.com/runetfreedom/russia-blocked-geosite
- Used for: the `category-ads-all` list (fetched from the `release` branch;
  the exact sha256 of the input is recorded in `manifest.json`).
- License: GNU General Public License v3.0 (see `LICENSE-GPL-3.0.txt`).

## 3. runetfreedom/russia-blocked-geoip — GPL-3.0

- Source: https://github.com/runetfreedom/russia-blocked-geoip
- Used for: upstream `geoip.dat`, filtered down to the categories listed in
  `categories.lock.json`.
- License: GNU General Public License v3.0 (see `LICENSE-GPL-3.0.txt`).
- The corresponding source is the upstream repository above plus the
  filtering scripts in `xray-manager/geodata-build/scripts/` (private repo;
  the exact input sha256 and filter category list are in `manifest.json`, so
  the output can be reproduced from the public upstream input).

Because the distributed `geoip.dat` is a filtered derivative of GPL-3.0 data,
the full GPL-3.0 text is included as `LICENSE-GPL-3.0.txt`. `geosite.dat`
contains a GPL-3.0-derived ads list and is distributed under the same terms
for that portion.

## 4. community.antifilter.download — community list

- Source: https://community.antifilter.download/list/domains.lst
- Used for: the `ru-blocked` category (core community part).
- No explicit license is published by the list maintainers. The list is a
  community-compiled set of blocked domains; attribution is given here and the
  exact sha256 of the fetched list is recorded in `manifest.json`.

If you are a rights holder and believe an entry is used incorrectly, open an
issue in the artifact repository and it will be reviewed.

## 5. Curated lists (`ru-blocked` additions)

The following curated additions were assembled for this project:

- `curation/libraries.txt` — online libraries;
- `curation/trackers.txt` — explicit tracker domains;
- `curation/extra.txt` — media/opposition sites missing upstream;
- `curation/deny/*` — domains deliberately excluded from `ru-blocked`.

These lists are provided under the MIT license of `xray-manager`
(Copyright (c) 2026 Evgeny Zhuravlev), without warranty of any kind.

## 6. No warranty

The artifacts are provided "as is", without warranty of any kind. Domain and
IP categorization is inherently approximate; use at your own risk. Nothing here
is legal advice, and inclusion of a domain does not imply any statement about
its content or legality.
