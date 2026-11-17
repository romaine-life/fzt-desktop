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

Produces an NSIS installer and MSI under `target/release/bundle/`.

## CI and releases

Forgejo runs CI from pipeline-templates' `rust` and `release` suites, with no workflow
here. A pull request runs rustfmt, clippy and the tests on Windows, and a release build
when packaging inputs change. A merge to main that changes the app publishes the next
`v0.1.N` with its signed `fzt-desktop` executable. The fzt-browser assets a release
embeds are the ones `dependencies.lock` pins; each fzt-browser release proposes moving
them forward as a take-up PR.

## Related

- [fzt-browser](https://github.com/romaine-life/fzt-browser) — source of `fzt.wasm` (downloaded at build time)
- [fzt-showcase](https://github.com/romaine-life/fzt-showcase) — reference for the CRT/DOS aesthetic
- [ambience](https://github.com/romaine-life/ambience) — entropy source for the pixel-art layer
