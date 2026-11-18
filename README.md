# fzt-desktop

Native Windows desktop surface hosting [fzt-automate](https://github.com/romaine-life/fzt-automate) + ambience pixel-art, built on [Tauri 2](https://tauri.app) with WebView2. Full architecture and decision thread in [CLAUDE.md](./CLAUDE.md).

## Develop

```sh
npm install
npm run tauri dev
```

First `tauri dev` compiles Tauri's Rust deps — expect a few minutes on a cold build.
`npm install` takes fzt-browser's WASM, JavaScript and CSS from its npm package
`@romaine-life/fzt-browser` on Forgejo and copies them into `src/`; it reads the package
with the token in `FORGEJO_PACKAGES_TOKEN` (on a home PC, the one
`romaine-auth home-token --role forgejo-packages` writes).

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
embeds come from the version of `@romaine-life/fzt-browser` that `package.json` pins; each
fzt-browser release proposes it as a take-up PR.

## Related

- [fzt-browser](https://github.com/romaine-life/fzt-browser) — source of `fzt.wasm` (its npm package)
- [fzt-showcase](https://github.com/romaine-life/fzt-showcase) — reference for the CRT/DOS aesthetic
- [ambience](https://github.com/romaine-life/ambience) — entropy source for the pixel-art layer
