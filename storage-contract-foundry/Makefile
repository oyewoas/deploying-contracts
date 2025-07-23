-include .env

.PHONY: all test clean deploy fund help install snapshot format anvil build verify

# Default values
DEFAULT_ANVIL_KEY := 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
DEFAULT_ACCOUNT := default

# Main targets
all: clean install build

# Clean the repo
clean:
	@echo "🧹 Cleaning..."
	forge clean

# Remove modules
remove:
	@echo "🗑️ Removing modules..."
	rm -rf .gitmodules && rm -rf .git/modules/* && rm -rf lib && touch .gitmodules && git add . && git commit -m "modules"

# Install dependencies
install:
	@echo "📦 Installing dependencies..."
	forge install foundry-rs/forge-std@v1.8.2 --no-commit

# Update Dependencies
update:
	@echo "🔄 Updating dependencies..."
	forge update

# Build contracts
build:
	@echo "🔨 Building contracts..."
	forge build

# Test contracts
test:
	@echo "🧪 Running tests..."
	forge test

# Run tests with verbose output
test-v:
	@echo "🧪 Running tests with verbose output..."
	forge test -vvv

# Run tests with gas reporting
test-gas:
	@echo "🧪 Running tests with gas reporting..."
	forge test --gas-report

# Run specific test
test-match:
	@echo "🧪 Running tests matching pattern..."
	forge test --match-test $(TEST)

# Snapshot
snapshot:
	@echo "📸 Creating snapshot..."
	forge snapshot

# Format code
format:
	@echo "🎨 Formatting code..."
	forge fmt

# Lint code
lint:
	@echo "🔍 Linting code..."
	forge fmt --check

# Start local anvil instance
anvil:
	@echo "🚀 Starting Anvil..."
	anvil -m 'test test test test test test test test test test test junk' --steps-tracing --block-time 1

# Deploy to local anvil
deploy-local:
	@echo "🚀 Deploying to local Anvil..."
	forge script script/Counter.s.sol:CounterScript --rpc-url http://localhost:8545 --private-key $(DEFAULT_ANVIL_KEY) --broadcast

# Deploy to Sepolia
deploy-sepolia:
	@echo "🚀 Deploying to Sepolia..."
	forge script script/Counter.s.sol:CounterScript --rpc-url $(SEPOLIA_RPC_URL) --private-key $(PRIVATE_KEY) --broadcast --verify --etherscan-api-key $(ETHERSCAN_API_KEY) -vvvv

# Deploy to Alfajores (Celo testnet)
deploy-alfajores:
	@echo "🚀 Deploying to Alfajores (Celo testnet)..."
	forge script script/Counter.s.sol:CounterScript --rpc-url $(ALFAJORES_RPC_URL) --private-key $(PRIVATE_KEY) --broadcast --verify --etherscan-api-key $(CELOSCAN_API_KEY) -vvvv
# forge create --rpc-url celo-alfajores --private-key $(PRIVATE_KEY) src/Counter.sol:Counter --verify

# Deploy to mainnet
deploy-mainnet:
	@echo "🚀 Deploying to mainnet..."
	forge script script/Counter.s.sol:CounterScript --rpc-url $(MAINNET_RPC_URL) --private-key $(PRIVATE_KEY) --broadcast --verify --etherscan-api-key $(ETHERSCAN_API_KEY) -vvvv

# Verify contract on Etherscan
verify:
	@echo "✅ Verifying contract..."
	forge verify-contract $(CONTRACT_ADDRESS) src/Counter.sol:Counter --chain-id $(CHAIN_ID) --etherscan-api-key $(ETHERSCAN_API_KEY) --constructor-args $(CONSTRUCTOR_ARGS)

# Verify contract on Celoscan
verify-alfajores:
	@echo "✅ Verifying contract on Celoscan..."
	forge verify-contract $(CONTRACT_ADDRESS) src/Counter.sol:Counter --chain-id 44787 --etherscan-api-key $(CELOSCAN_API_KEY)

# Get contract size
size:
	@echo "📏 Contract size:"
	forge build --sizes

# Get gas usage
gas:
	@echo "⛽ Gas usage:"
	forge test --gas-report

# Coverage
coverage:
	@echo "📊 Running coverage..."
	forge coverage

# Coverage with lcov
coverage-lcov:
	@echo "📊 Running coverage with lcov..."
	forge coverage --report lcov

# Fuzz testing
fuzz:
	@echo "🎲 Running fuzz tests..."
	forge test --fuzz-runs 1000

# Invariant testing
invariant:
	@echo "🔄 Running invariant tests..."
	forge test --invariant-runs 1000

# Debug specific test
debug:
	@echo "🐛 Debugging test..."
	forge test --match-test $(TEST) -vvvv

# Show help
help:
	@echo "Available commands:"
	@echo "  all              - Clean, install, and build"
	@echo "  clean            - Clean the repo"
	@echo "  install          - Install dependencies"
	@echo "  update           - Update dependencies"
	@echo "  build            - Build contracts"
	@echo "  test             - Run tests"
	@echo "  test-v           - Run tests with verbose output"
	@echo "  test-gas         - Run tests with gas reporting"
	@echo "  test-match       - Run specific test (use TEST=pattern)"
	@echo "  snapshot         - Create snapshot"
	@echo "  format           - Format code"
	@echo "  lint             - Check code formatting"
	@echo "  anvil            - Start local Anvil instance"
	@echo "  deploy-local     - Deploy to local Anvil"
	@echo "  deploy-sepolia   - Deploy to Sepolia (requires env vars)"
	@echo "  deploy-alfajores - Deploy to Alfajores (requires env vars)"
	@echo "  deploy-mainnet   - Deploy to mainnet (requires env vars)"
	@echo "  verify           - Verify contract on Etherscan"
	@echo "  verify-celo      - Verify contract on Celoscan"
	@echo "  size             - Show contract sizes"
	@echo "  gas              - Show gas usage"
	@echo "  coverage         - Run coverage"
	@echo "  coverage-lcov    - Run coverage with lcov"
	@echo "  fuzz             - Run fuzz tests"
	@echo "  invariant        - Run invariant tests"
	@echo "  debug            - Debug specific test (use TEST=pattern)"
	@echo "  help             - Show this help message"