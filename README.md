# ICP Prediction Market Layer 🎯

A decentralized binary options trading platform built on the Internet Computer Protocol (ICP), allowing users to make price direction predictions on cryptocurrency pairs.

## Overview 🌟

The Binary Options Market is a proof-of-concept prediction market that leverages ICP's infrastructure to create a transparent and decentralized trading environment. Users can participate by predicting whether an asset's price will go up or down within a specified timeframe.

### Key Features
- 📈 Resolved with price feeds via HTTP Outcalls
- ⚡ 30-second trading windows
- 🎲 Entire-pool reward/loss per correct/incorrect prediction
- 🔒 Secure identity management via Internet Identity
- 💱 Support for multiple cryptocurrency pairs

## Demo 🎮

![Trading Interface](./docs/images/UI-demo.png)

- [Demo 1](https://drive.google.com/file/d/1C3wPzyXKbTXys8lZsR3-WREsOCCNbdZB/view?usp=sharing)
- [Demo 2](https://drive.google.com/file/d/1P47yfKLGNXfwjS3YHDA9k1iZrf9nMMRy/view?usp=sharing)

![Diagram](./docs/images/diagram.png)
## Architecture 📐

The project consists of two main components:

1. **Binary Option Market Canister** (`canisters/binary_option_market/`)
   - Core trading/managing logic
   - HTTP Outcalls for price feeds
   - State management
   - Account management

2. **Frontend** (`icp-asset/`)
   - React/Next.js interface
   - Internet Identity integration
   - Real-time updates

## Technical Stack 🛠

- **Backend**: Motoko
- **Frontend**: Next.js, TypeScript, Chakra UI
- **Identity**: Internet Identity
- **Price Feeds**: HTTP Outcalls
- **State Management**: Redux Toolkit

## Getting Started 🚀

### Prerequisites
- dfx CLI
- Node.js >= 14
- NPM

### Local Development

1. Start the local replica:

```bash
cd oreka/

dfx start --clean
```

2. Deploy the Binary Option Market canister with initial arguments:

```bash
export MINTER=$(dfx --identity anonymous identity get-principal)
export DEFAULT=$(dfx identity get-principal)

# deploy icp_ledger_canister dependency first
dfx deploy icp_ledger_canister --argument "(variant { Init =
record {
     token_symbol = \"ICRC1\";
     token_name = \"L-ICRC1\";
     minting_account = record { owner = principal \"${MINTER}\" };
     transfer_fee = 10_000;
     metadata = vec {};
     initial_balances = vec { record { record { owner = principal \"${DEFAULT}\"; }; 10_000_000_000; }; };
     archive_options = record {
         num_blocks_to_archive = 1000;
         trigger_threshold = 2000;
         controller_id = principal \"${MINTER}\";
     };
 }
})"

# deploy binary_option_market
dfx deploy binary_option_market --argument '(12.0, 1734503362)'

# optional: deploy test canister
dfx deploy binary_option_market_test
dfx canister call binary_option_market_test test
```

3. Install frontend dependencies:

```bash
# deploy the internet identity
dfx deps deploy

cd icp-asset
npm install --legacy-peer-deps
```

4. Start the frontend development server:

```bash
npm run dev
```

## Project Status 📊

Current Features:
- ✅ Core prediction market contracts
- ✅ HTTP Outcalls price feed integration
- ✅ Basic trading interface
- ✅ Internet Identity integration

Roadmap:
- 🔄 Advanced trading features
- 🔄 Multi-asset support
- 🔄 Shared liquidity infrastructure

## Future Development 🔮

We have exciting plans to enhance the platform:

1. **ChainFusion Integration**
   - Implementation of ChainFusion as an oracle solution
   - Support for EVM-compatible smart contracts

2. **Shared Liquidity Infrastructure**
   - Cross-chain liquidity pools
   - Unified prediction market ecosystem

## Contributing 🤝

Contributions are welcome! Please read our contributing guidelines before submitting PRs.

## License 📄

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments 🙏

- DFINITY Foundation
- Internet Computer Community

## Contact 📧

For questions and support, please open an issue or reach out to the maintainers.

---

Built with ❤️ for the Internet Computer ecosystem.
