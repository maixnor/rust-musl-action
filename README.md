# GitHub Action for Rust and MUSL

Action provides an environment with stable Rust 1.60, MUSL and x86_64-unknown-linux-musl target.

## Usage

To compile a rust binary/library with x86_64-unknown-linux-musl target:
Example include also the way to upload the final binary as artifact.

```yaml
name: Rust-static-build
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]
env:
  CARGO_TERM_COLOR: always
  BUILD_TARGET: x86_64-unknown-linux-musl
  BINARY_NAME: <binary_name>
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Build-musl
      uses: gmiam/rust-musl-action@master
      with:
        args: cargo build --target $BUILD_TARGET --release
    - uses: actions/upload-artifact@v2
      with:
        name: ${{ env.BINARY_NAME }}
        path: target/x86_64-unknown-linux-musl/release/${{ env.BINARY_NAME }}*
```

## License

The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).

