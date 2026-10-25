# bun-ssh

The `ssh` plugin of the Aphrody Bun fork: the `bun-ssh` executable that
`bun ssh` dispatches to (`src/runtime/cli/plugin_command.rs` in
[aphrody-labs/bun](https://github.com/aphrody-labs/bun)).

Imported from aphrody-labs/bun commit `f31829d8aa36e9f34e662c8a9e5edf6e25705c86` (src/plugins/ssh, src/ssh and vendor/russh-sftp). That repository keeps the
earlier history.

## Install

Nothing to install: the first `bun ssh ...` downloads `bun-ssh-<target>` from the
release of the running bun, checks it against that release's `SHA256SUMS.txt`
and caches it in the plugin directory. A `bun-ssh` next to the bun executable
takes precedence.

## Build from source

This workspace path-depends on crates of the Bun checkout, so it builds only
mounted in it as `plugins/ssh` (an optional submodule, `update = none`):

```sh
git -C <bun checkout> submodule update --init --checkout --recursive plugins/ssh
bun bd --target=plugins          # build/<profile>/bun-ssh next to bun
# or directly:
cd <bun checkout>/plugins/ssh && cargo build --locked --profile plugin -p bun_plugin_ssh --bin bun-ssh
```

The toolchain is the Bun checkout's `rust-toolchain.toml`. `Cargo.lock` was
derived from the Bun workspace lockfile, so dependency versions match what the
fork built before the move.
