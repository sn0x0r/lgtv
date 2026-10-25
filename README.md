# lgtv

Clean-up and a custom launcher for an LG OLED65G1 (webOS 6, firmware 03.53.45), based on [shipstuff/tvunlock](https://github.com/shipstuff/tvunlock). No root.

- [launcher/](launcher/): a minimal dark home screen, sideloaded with LG Developer Mode.
- [docs/DEVMODE.md](docs/DEVMODE.md): how to build it and put it on the TV.

Each push that touches `launcher/` builds the `.ipk` in GitHub Actions (the "Build launcher" workflow, artifact `launcher-ipk`), so you don't need Node installed to get it.
