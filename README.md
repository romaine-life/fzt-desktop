# fzt-desktop

Native Windows desktop surface hosting [fzt-automate](https://github.com/romaine-life/fzt-automate) + ambience pixel-art, built on [Tauri 2](https://tauri.app) with WebView2. Full architecture and decision thread in [CLAUDE.md](./CLAUDE.md).

## Develop

```sh
npm install
npm run fetch-fzt
npm run tauri dev
```

First `tauri dev` compiles Tauri's Rust deps — expect a few minutes on a cold build.
Set `FORGEJO_TOKEN` to a token that can read the fzt-browser release before fetching
its WASM, JavaScript and CSS assets from Forgejo.

## Build

```sh
npm run tauri build
```

Produces an NSIS installer and MSI under `src-tauri/target/release/bundle/`.
Forgejo CI builds and signs the app and both installers on pull requests and main.

## Release

After main's build passes, publish the next `v0.1.N` release on Forgejo:

```powershell
Invoke-RestMethod -Method Post -Uri 'https://forgejo.romaine.life/api/v1/repos/romaine-life/fzt-desktop/actions/workflows/ci.yml/dispatches' -Headers @{ Authorization = "token $env:FORGEJO_TOKEN" } -ContentType application/json -Body '{"ref":"main"}'
```

The workflow publishes the signed NSIS installer, MSI and `fzt-desktop.exe` after
the build succeeds. Installer filenames keep Tauri's existing naming scheme.

## Related

- [fzt-browser](https://github.com/romaine-life/fzt-browser) — source of `fzt.wasm` (downloaded at build time)
- [fzt-showcase](https://github.com/romaine-life/fzt-showcase) — reference for the CRT/DOS aesthetic
- [ambience](https://github.com/romaine-life/ambience) — entropy source for the pixel-art layer
