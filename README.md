# Terraformer Token Sale

This repository reflects the core contracts of the launchpad element of Terraformer.

The used contracts are forked from [Pylon Protocol](https://www.pylon.money/) and are using the

Gateway Swap
Cap-Fixed Strategy

contracts.

## Development

### Contract Verification

#### gateway_strategy_fixed.wasm 

Checksum: 0425b2a5e7b975a5d77caf3a13fac82a76248914ece3eb5c5e463a9290f28793

https://lcd.terra.dev/wasm/codes/1325

{"height":"5397357","result":{
"code_id": "1325",
"code_hash": "BCWypee5daXXfK86E/rIKnYkiRTs4+tcXkY6kpDyh5M=",
"creator": "terra16k0mnlqd36a4v3t3m62057wkxjxy46s7ppjj4m"
}}

Base64 to Hex of BCWypee5daXXfK86E/rIKnYkiRTs4+tcXkY6kpDyh5M=

0425b2a5e7b975a5d77caf3a13fac82a76248914ece3eb5c5e463a9290f28793

#### gateway_swap.wasm

Checksum: cd1d9825d61a18f4ed07f88c4bf7b930372e751927b545a9f2e21d4f4934d513

https://lcd.terra.dev/wasm/codes/1326

{"height":"5397412","result":{
"code_id": "1326",
"code_hash": "zR2YJdYaGPTtB/iMS/e5MDcudRkntUWp8uIdT0k01RM=",
"creator": "terra16k0mnlqd36a4v3t3m62057wkxjxy46s7ppjj4m"
}}

Base64 to Hex of BCWypee5daXXfK86E/rIKnYkiRTs4+tcXkY6kpDyh5M=

cd1d9825d61a18f4ed07f88c4bf7b930372e751927b545a9f2e21d4f4934d513

### Environment Setup

- Rust v1.44.1+
- `wasm32-unknown-unknown` target
- Docker

1. Install `rustup` via https://rustup.rs/

2. Run the following:

```sh
rustup default stable
rustup target add wasm32-unknown-unknown
```

3. Make sure [Docker](https://www.docker.com/) is installed

### Unit / Integration Tests

Each contract contains Rust unit and integration tests embedded within the contract source directories. You can run:

```sh
cargo unit-test
cargo integration-test
```

### Compiling

After making sure tests pass, you can compile each contract with the following:

```sh
RUSTFLAGS='-C link-arg=-s' cargo wasm
cp ../../target/wasm32-unknown-unknown/release/cw1_subkeys.wasm .
ls -l cw1_subkeys.wasm
sha256sum cw1_subkeys.wasm
```

#### Production

For production builds, run the following:

```sh
docker run --rm -v "$(pwd)":/code \
  --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target \
  --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
  cosmwasm/workspace-optimizer:0.12.3
```

This performs several optimizations which can significantly reduce the final size of the contract binaries, which will
be available inside the `artifacts/` directory.
