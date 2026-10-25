# Launcher source

Copied from [shipstuff/tvunlock](https://github.com/shipstuff/tvunlock) `launcher/` at commit `721bd34a0ef60ea7171411063717612955f03dfb`, which in turn vendors [partridgeworks/webos-launcher](https://github.com/partridgeworks/webos-launcher), commit `1e2c39b9a988ceb1b258e40e3592bda84a2aa076`.

Changes for this TV (LG OLED65G1, webOS 6, firmware 03.53.45):

- Hulu and Peacock (US only) are no longer in the default Apps row. They stay in the catalogue.
- No root helper is installed, so the LG Home tile opens LG Home (`com.webos.app.home`) directly, and the Homebrew option in Settings stays off.

The build already targets Chrome 79, the engine in webOS 6. Install steps are in [docs/DEVMODE.md](../docs/DEVMODE.md).

```sh
npm ci --ignore-scripts
npm run build
npm run package
```

See [LICENSE](LICENSE) and [third-party notices](THIRD_PARTY_NOTICES.md). Keep per-TV catalogs in the git-ignored `src/config/catalog.local.ts`. Never add a TV address or key to source.
