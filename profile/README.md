<div align="center">
  <img src="https://avatars.githubusercontent.com/u/325925498?s=140" width="70" alt="" />
  <h1>Angular Native</h1>
  <p><strong>Angular on real native views, with the core in Rust.</strong></p>
  <p>
    <a href="https://angular-native.dev">Documentation</a> ·
    <a href="https://github.com/Angular-Native/angular-native">Source</a> ·
    <a href="https://github.com/Angular-Native/angular-native/discussions">Discussions</a>
  </p>
</div>

---

Zoneless Angular with signals, running on an embedded JS engine. The UI tree,
the layout and the mounting onto real native views are Rust's job. No DOM, no
WebView, no zone.js — one core for iOS, Android, macOS, the TV, the headset and
both watches.

```text
  engine thread                                  UI thread
  Angular (JS) -> Renderer2 -> __an_dom          CADisplayLink / Choreographer
      -> binary buffer -> ShadowTree             -> MountSide -> HostRenderer
         -> taffy layout -> diff                    (UIKit / android.view / AppKit)
         -> Frame { MountOp[] } ------------------>
```

An `<an-switch>` **is** a `UISwitch` and a `MaterialSwitch`. Accessibility, IME,
scrolling and the system look come free, because the system drew them.

### Repositories

| Repository | What it is |
|---|---|
| [`angular-native`](https://github.com/Angular-Native/angular-native) | The monorepo: the Rust core, the eight hosts, the npm packages, the CLI, the examples and the docs site |
| [`.github`](https://github.com/Angular-Native/.github) | This profile and the shared community health files |

It is one repository on purpose. The Rust crates and the npm packages ship as a
single version and are checked together — `scripts/check-all.sh` runs the whole
device-free suite in one place, and splitting it would mean keeping the
duplicated primitive and style lists in sync across repositories instead of
across directories.

### Getting started

```bash
cargo install --path crates/an-cli   # or: cargo an dev, inside the monorepo
an init && an add ios && an ios
```

`an` never touches `src/main.ts` or `angular.json`, so `ng build` and `ng serve`
keep working on the same project.

### License

MIT.
