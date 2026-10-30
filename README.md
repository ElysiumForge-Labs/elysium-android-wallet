# elysium-android-wallet

Native Android wallet (**Koro**) for **Kinetiq's Elysium testnet** — BIP-39 vault on device, live native balances over JSON-RPC, and an in-app dapp browser with EIP-1193 approvals.

Part of [ElysiumForge Labs](https://github.com/ElysiumForge-Labs).

> **Independent research repository. Testnet only.** Not affiliated with, endorsed by, or sponsored by Kinetiq or Hyperliquid. Accounts, balances, and transactions here target Elysium and other public test networks. Test assets have no monetary value. This project has not been independently audited. Do not import a mainnet recovery phrase.

## Features

| Capability | Detail |
| --- | --- |
| Create / import | 12-word BIP-39 create; 12- or 24-word import; derivation `m/44'/60'/0'/0/0` |
| Vault | AES-256-GCM; wrapping key in Android Keystore when available |
| Seed reveal | Biometric or device-credential prompt |
| RPC | `eth_chainId` check, block number, native balance with integer wei math |
| Dapp browser | EIP-1193 `window.ethereum` (`isKoro`; `isMetaMask` for detection-only sites) |
| Approvals | Explicit prompts for connect, `personal_sign`, chain switch, and `eth_sendTransaction` |

Portfolio prices, the NFT grid, the activity feed, and the swap quote are sample UI. They are not wired to a price feed or an exchange.

## Networks

Elysium Testnet is the default. The selected network is stored separately from the wallet vault.

| Network | Chain ID | Native | RPC |
| --- | --- | --- | --- |
| Elysium Testnet | `99801` | HYPE | `https://testnet-rpc.elysium.kinetiq.xyz` |
| HyperEVM Testnet | `998` | HYPE | `https://rpc.hyperliquid-testnet.xyz/evm` |
| Sepolia | `11155111` | ETH | `https://rpc.sepolia.org` |
| Arbitrum Sepolia | `421614` | ETH | `https://sepolia-rollup.arbitrum.io/rpc` |

Custom EVM networks can be registered locally (unique id, positive chain id, `http`/`https` RPC). Before a balance read or broadcast, the client compares the node's `eth_chainId` with the selected network; a mismatch blocks the send.

- Explorer: [elysium.kinetiq.xyz/testnet-explorer](https://elysium.kinetiq.xyz/testnet-explorer)
- Faucet: [elysium.kinetiq.xyz/testnet-faucet](https://elysium.kinetiq.xyz/testnet-faucet)

## Stack

| Item | Value |
| --- | --- |
| Language | Kotlin |
| UI | Jetpack Compose |
| Build | Gradle Kotlin DSL |
| Min / target SDK | 24 / 36 |
| Version | 1.0 (`versionCode` 1) |
| Application ID | `com.aistudio.elysiumwallet.vqzrmp` |

## Getting started

### Prerequisites

- Android Studio (recent stable) with JDK 17+
- Android SDK platform matching `compileSdk` 36
- A physical device or emulator (API 24+)

### Build and run

```sh
# From the repository root
./gradlew :app:assembleDebug
./gradlew :app:installDebug
```

Open the project in Android Studio and run the `app` configuration for an interactive session.

### Tests

```sh
./gradlew :app:testDebugUnitTest
```

Unit coverage includes vault cipher, network registry, RPC client, wallet vault repository, and dapp browser helpers.

## Scope

Wired to chain data or the vault today: create / import / switch / back up wallets; network selection and custom networks; native balance refresh; dapp connect, `personal_sign`, chain switch, and `eth_sendTransaction`.

## Security

- Treat the recovery phrase as the wallet. The app cannot restore funds if the phrase and device vault are both lost.
- Never import a mainnet seed into this build.
- Keystore-backed wrapping is preferred; behavior depends on device hardware and enrollment.

## License

See repository files for license terms.
