# Contributing

Everything lives in one repository, [`angular-native`](https://github.com/Angular-Native/angular-native):
the Rust crates, the npm packages, the CLI, the examples and the docs site. A
change usually touches more than one of them, which is why they are not split.

## Before you open a pull request

```bash
./scripts/check-all.sh
```

That is the gate. It runs the Rust tests, the duplicated-list checks, the
example apps through the headless bridge, the accessibility trees, the plugins,
an external Angular project, a real macOS `.app` that is launched and
screenshotted, and the two cross-compilations. A script that cannot do its job
prints `skipped` rather than passing quietly, so a `skipped` line is
information, not a failure.

Scripts ending in `-device.sh` need a plugged-in phone or watch and are not part
of `check-all.sh`.

## The lists that drift silently

Several lists are necessarily duplicated across languages, and drift in any of
them fails without an error — an unrecognised prop simply does nothing. Adding a
primitive or a prop means touching every link:

- **Primitive names** — the directive selector in `packages/primitives`, then
  `NATIVE_KINDS`, then `KIND` in the runtime, then `kind_from_byte` in the
  bridge. Guarded by `scripts/check-kinds.sh`.
- **Style names** — the JS list against the core's. Guarded by
  `scripts/check-styles.sh`.
- **Props reaching every host** — a directive prop must be read by every host
  crate, not just the one you tested on. Guarded by `scripts/check-wrapper.sh`.
- **The site's address** — `DOCS_URL` at the root is the one place it is
  decided. Astro reads that file; the README's links, the `homepage` of every
  npm package and the URLs inside the CLI's error strings are written out
  because they cannot share a variable. Guarded by
  `scripts/check-docs-url.sh`, which rewrites all of them with `--fix`. Never
  edit one of those links by hand.

Run the relevant check script directly; it is much faster than finding out on a
device.

## Debugging without a simulator

```bash
cargo an build examples/hello-angular
cargo run -p an-bridge --example headless -- build/bundle/hello-angular/main.js 6
```

`headless` assembles the whole pipeline except the platform: it evaluates the
bundle, advances frames on a fake clock, simulates press/drag/scroll/back and
prints the resolved tree with positions.

## Conventions

Commit subjects are prose sentences, mostly lowercase, sometimes with a
`type(scope):` prefix (`fix(checks):`, `docs(site):`, `feat(examples):`) and
often without. They describe the behaviour change, not the files touched.

Comments carry the *reasoning* — why a target is `cfg`'d out, why a name was
frozen, why a list is duplicated. Match that register: explain the constraint,
not the mechanics.

## Discussing a change first

For anything that moves an architectural line, open a
[discussion](https://github.com/Angular-Native/angular-native/discussions)
before writing the code. The `Decisions` section of `README.md` explains why
almost everything is the way it is, and it is the right place to argue with.
