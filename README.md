# elysium-android-wallet

Native Android wallet (**Koro**) for **Kinetiq's Elysium testnet**. Creates and restores BIP-39 accounts on device, reads live native balances over JSON-RPC, and lets dapps request connections, signatures, and transactions through an in-app browser.

Part of [ElysiumForge Labs](https://github.com/ElysiumForge-Labs).

> **Independent research repository. Testnet only.** Not affiliated with, endorsed by, or sponsored by Kinetiq or Hyperliquid. Accounts, balances, and transactions here are for Elysium and other public test networks. Test assets have no monetary value. This project has not been independently audited. Do not import a mainnet recovery phrase.

## Overview

| Capability | Detail |
| --- | --- |
| Wallet create / import | 12-word BIP-39 create; 12- or 24-word import; derivation `m/44'/60'/0'/0/0` |
| Vault | AES-256-GCM; wrapping key in Android Keystore when available |
| Seed reveal | Biometric or device-credential prompt |
| RPC | `eth_chainId` check, block number, native balance with integer wei math |
| Dapp browser | EIP-1193 `window.ethereum` (`isKoro`, plus `isMetaMask` for detection-only sites) |
| Approvals | Explicit prompts for connect, `personal_sign`, chain switch, and `eth_sendTransaction` |

Portfolio prices, the NFT grid, the activity feed, and the swap quote are sample UI and do not come from a price feed or an exchange.

## Networks

Elysium Testnet is the default. The selected network is stored separately from the wallet.

| Network | Chain ID | Native | RPC |
| --- | --- | --- | --- |
| Elysium Testnet | `99801` | HYPE | `https://testnet-rpc.elysium.kinetiq.xyz` |
| HyperEVM Testnet | `998` | HYPE | `https://rpc.hyperliquid-testnet.xyz/evm` |
| Sepolia | `11155111` | ETH | `https://rpc.sepolia.org` |
| Arbitrum Sepolia | `421614` | ETH | `https://sepolia-rollup.arbitrum.io/rpc` |

Custom EVM networks can be registered locally (unique id, positive chain id, `http`/`https` RPC). Before a balance read or broadcast, the client compares the node’s `eth_chainId` with the selected network; a mismatch blocks the send.

Explorer: [elysium.kinetiq.xyz/testnet-explorer](https://elysium.kinetiq.xyz/testnet-explorer) · Faucet: [elysium.kinetiq.xyz/testnet-faucet](https://elysium.kinetiq.xyz/testnet-faucet)

## Stack

| Item | Value |
| --- | --- |
| Version | 1.0 (`versionCode` 1) |
| Application ID | `com.aistudio.elysiumwallet.vqzrmp` |
| Build | Gradle Kotlin DSL (Android) |

## Scope today

Wired to chain data or the vault: create / import / switch / back up wallets; network selection and custom networks; native balance refresh; dapp connect, `personal_sign`, chain switch, and `eth_sendTransaction`.

## License

See repository files for license terms. Treat the recovery phrase as the wallet; the app cannot restore it if the phrase and device vault are both lost.
