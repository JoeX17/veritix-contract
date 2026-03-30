default: build

all: test

test: build
	cargo test

build:
	stellar contract build
	# stellar contract build outputs to wasm32v1-none (Soroban's canonical target).
	# wasm32-unknown-unknown is only used for `cargo test` and clippy, not for WASM artifacts.
	@ls -l ../../target/wasm32v1-none/release/*.wasm

build-logs:
	cargo build --profile release-with-logs --target wasm32-unknown-unknown
	@ls -l ../../target/wasm32-unknown-unknown/release-with-logs/*.wasm

test-logs:
	cargo test --profile release-with-logs

fmt:
	cargo fmt --all

clean:
	cargo clean

# Deploy to localnet (set STELLAR_NETWORK=testnet for testnet)
deploy:
	bash $(CURDIR)/../../../scripts/deploy.sh

# Invoke a contract function. Usage: make invoke ARGS="balance alice"
invoke:
	bash $(CURDIR)/../../../scripts/invoke.sh $(ARGS)
