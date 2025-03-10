# Bridge-Smart-Contract

This repository contains the code to deploy and initialize the smart contracts for the Wrapped Hydra Token, Wrapped Hydra Staking and Liquidity Staking on Uniswap.
## Development

```bash
# Install dependencies
$ npm ci
```

```bash
# Compile contract(s)
$ npm run compile
```

## Deployment of Smart Contracts

The `scripts/deploy.js` file contains the code to deploy the smart contracts. This script logs the different smart contract that are deployed. The addresses can be used later to initialize the proxies and to set-up the UI. Ensure that there is sufficient amount of ether in the wallet. 

The following environment variables are required:
- INFURA_KEY: The Infura key to interact with the Ethereum network.
- WALLET_PASSPHRASE: The passphrase that gives access to your Ethereum wallet.

```bash
# Deploy
$ export INFURA_KEY=[your_infura_key]
$ export WALLET_PASSPHRASE=[your_passphrase]
$ export NETWORK=[mainnet|rinkeby|ropsten]
$ npm run deploy
```

## Initialization of Smart Contracts

The proxy pattern requires the separate initialization of the different smart contracts instead of running constructor functions.

Each smart contract needs specific information for initialization. The scripts are bundled in two parts: the initialization of the Wrapped Hydra token contract (`scripts/initWrappedHydra.js`) and the initialization of the staking contracts (`scripts/initStaking.js`).

**The environment variables from deployment need to persist for subsequent calls**

### Wrapped Hydra

The owner and the signer are required to initialize the Wrapped Hydra contract. Currently, they are the first and the second account of the wallet. The **owner** can change the smart contract logic and the smart contract owner. The **signer** approves the minting of new Hydra's. 

The following environment variables are required as well:
- WHYD_ADDRESS: The address of the Wrapped Hydra smart contract.

```bash
# Deploy
$ export WHYD_ADDRESS=[whyd_contract_address]
$ npm run init-whyd
```

### Wrapped Hydra Staking

After the Wrapped Hydra token contract has been initialized, the Wrapped Hydra staking contract can be initialized as well. The initializer has to possess enough Wrapped Hydra to cover the initial rewards. 

The following environment variables are required as well:
- WHYD_STAKING_ADDRESS: The address of the Wrapped Hydra staking smart contract.

```bash
# Deploy
$ export WHYD_STAKING_ADDRESS=[whyd_staking_contract_address]
$ npm run init-whyd-staking
```

### Liquidity Staking

After the liquidity pool has been opened on Uniswap, the liquidity staking contract can be initialized as well. The sender has to possess enough Wrapped Hydra to cover the rewards.

The following environment variables are required as well:
- PAIR_ADDRESS: The address of the Uniswap Liquidity Pool Token representing the pair within the pool.
- STAKING_ADDRESS: The address of the liquidity staking smart contract.

```bash
# Deploy
$ export PAIR_ADDRESS=[uniswap_pool_pair_address]
$ export STAKING_ADDRESS=[liquidity_staking_contract_address]
$ npm run init-liquidity-staking
```

### 
```bash
# Deploy
$ npm test
```