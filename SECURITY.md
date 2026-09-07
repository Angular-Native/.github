# Security policy

## Supported versions

The project is pre-1.0. Only the latest release on `main` receives security
fixes.

## Reporting a vulnerability

Report privately through GitHub — open a
[security advisory](https://github.com/Angular-Native/angular-native/security/advisories/new)
on the repository. Please do not open a public issue for a vulnerability.

Include what you can: the affected crate or package, the platform target, a
reproduction, and the impact you believe it has. You will get an
acknowledgement, and a fix or an explanation of why it is not one, before any
public disclosure.

## What is in scope

The runtime surface is the interesting part: the QuickJS bridge and its binary
protocol, the native module boundary (`an-bridge`), the plugin surface, the
keychain and biometrics plugins, and the CLI's signing path.

Out of scope: anything requiring a device the attacker already controls at root,
and the example apps under `examples/`, which exist to be driven by the checks.
