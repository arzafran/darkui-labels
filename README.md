# darkui label index

This repository holds a small signed JSON index that tells a darkui handheld where to find the
cartridge label for a game and how to crop it. It contains no images. The device downloads each
scan from the original site listed in the entry, checks its SHA-256 and pixel size, crops and
composes the label on the device, and keeps the attribution next to the result.

- `index.json`: version 1, 435 entries, SHA-256 `0873194e062e20be2d8a990628bba85b4cb4f8992c8f85bbb93f22cb2af80b90`
- `index.json.sig`: raw 64-byte Ed25519 signature over the exact bytes of `index.json`
- built from `assets/labels/catalog.json` (SHA-256 `efcf6e11436c30821e8cb763f0c1ac5e824cb159f536f97f42bb14802b1be183`) in the darkui repository

Verify a download with the public key shipped in every darkui image
(`/usr/share/darkui/update-ed25519.pub.pem`):

```sh
openssl pkeyutl -verify -pubin -inkey update-ed25519.pub.pem -rawin -in index.json -sigfile index.json.sig
```

## Sources and attribution

Every entry names the original image (`url`), who made or hosts it (`source`, `contributor`) and the
licence note recorded when it was reviewed (`license`). The artwork stays the property of its owners;
public availability is not a blanket redistribution licence, which is why nothing is rehosted here.
Images are fetched by each device from the original host and are never stored in this repository.

Entries by system: ARCADE 3, FC 1, GB 151, GBA 151, GBC 100, GG 3, MD 5, NGP 2, NGPC 3, PCE 2, PS 7, SFC 1, SMS 2, WS 2, WSC 2.

Source hosts:

- cdn.shopify.com: 1
- gamesdb-images.launchbox.gg: 116
- gbhwdb.gekkio.fi: 50
- i.ebayimg.com: 3
- images.launchbox-app.com: 246
- kabukido-neo-japonisme-nerdy-store.com: 1
- raw.githubusercontent.com: 8
- retrospekt.com: 2
- shop.mandmgames.com: 1
- www.agil-retrogaming.fr: 1
- www.dialupgames.com: 1
- www.j4u.co.jp: 1
- www.mvs-scans.com: 3
- www.pjsgames.com: 1

Licence notes (as reviewed):

- 205 x Copyright respective rights holders; public source for personal collection use, no blanket redistribution license.
- 86 x Game artwork: original rights holders; source image supplied by LaunchBox Games Database
- 38 x CC-BY-SA-4.0
- 27 x Game-specific fan recreation; underlying artwork copyright respective holders; no blanket reuse license asserted.
- 24 x Copyright respective artwork and photograph rights holders; publicly accessible source, no blanket redistribution permission claimed.
- 15 x Copyright respective rights holders; publicly accessible source for personal collection use; no blanket redistribution license.
- 8 x Copyright respective rights holders; public reference image; no blanket redistribution license.
- 8 x Original game artwork; scan author permits digital imports
- 7 x CC BY-SA 4.0; game artwork belongs to respective rights holders.
- 6 x Game artwork and retailer photography: respective rights holders; no blanket redistribution license.
- 5 x CC-BY-SA-4.0 (source photograph and this crop); cartridge label artwork belongs to its respective rights holders.
- 4 x Game artwork: original rights holders; image supplied by LaunchBox Games Database
- 1 x Copyright respective rights holders; public image availability does not establish a redistribution license.
- 1 x Retailer photograph and underlying label copyright respective holders; no blanket reuse license asserted.

Gekkio's Game Boy Hardware Database photographs are CC BY-SA 4.0; a label derived from one keeps the
photographer's credit in the sidecar the device writes next to it.

## Updating

Run `make label-index` in the darkui repository after the reviewed catalog changes, then commit the
three files it writes. A device re-checks this index at most once a day.
