CCIP: Chainlink Cross-Chain Interoperability Protocol Starter Kit

This project demonstrates several basic and advanced use cases of Chainlink's Cross-Chain Interoperability Protocol (CCIP), the secure, decentralized standard for cross-chain communication and value transfer.

📄 Table of Contents
    1. What is Chainlink CCIP?
    2. Prerequisites
    3. Getting Started
    4. Key Use Case Examples
    5. Testing and Faucet
    6. Custom Token Pool Configuration

1. What is Chainlink CCIP?

The Chainlink Cross-Chain Interoperability Protocol (CCIP) provides a single, simple interface through which decentralized applications (dApps) and Web3 developers can securely meet all their cross-chain needs.
With CCIP, you can:
    • Transfer Supported Tokens: Move tokens across different blockchain networks securely.
    • Send Arbitrary Messages (Data): Send any custom data or instructions from a contract on one chain to a contract on another.
    • Send Messages and Tokens (Programmable Transfers): Combine token transfer with execution instructions in a single, atomic transaction.

For developers, CCIP can be treated as a secure "black-box" component, requiring interaction only with the Router contract on the source chain.

2. Prerequisites

Before starting, ensure you have the following installed:
    • Node.js (v18+) and npm.
    • Hardhat or Foundry development environment.
    • Access to an RPC URL for the desired Testnet chains (e.g., Ethereum Sepolia, Arbitrum Sepolia).

Environment Setup
Create an environment variable file (.env or .env.enc) and configure the following, ensuring you have Testnet ETH (for gas) and Testnet LINK (to pay CCIP transfer fees) for your source chain:

Code snippet
# Example Environment Variables
# RPC URLs
ETHEREUM_SEPOLIA_RPC_URL=...
ARBITRUM_SEPOLIA_RPC_URL=...

# Your Wallet Private Key (for deployment and signing transactions)
PRIVATE_KEY=...

3. Getting Started
    1. Clone the Repository:
       Bash
       git clone https://github.com/Hashbury1/CCIP.git
       cd CCIP
    2. Install Dependencies:
       Bash
       npm install  # For Hardhat
       # or
       forge install  # For Foundry
    3. Compile Contracts:
       Bash
       npx hardhat compile # For Hardhat
       # or
       forge build # For Foundry

4. Key Use Case Examples
The repository includes scripts to demonstrate various CCIP functionalities. You can run these examples using Hardhat tasks or Foundry scripts, where each example corresponds to a distinct cross-chain scenario.

Example
Scenario
Fee Token
Smart Contracts Used

Example 1
Transfer CCIP Test Tokens from EOA to EOA.
Optional
None (direct task call)

Example 2
Transfer Tokens from EOA to a Smart Contract.
Optional
BasicTokenReceiver.sol

Example 3
Transfer Token(s) from a Smart Contract to any destination.
Optional
BasicTokenSender.sol

Example 4
Send & Receive Tokens and Data in a single transaction.
LINK or Native
TokenAndDataSender.sol, TokenAndDataReceiver.sol

Example 5
Send & Receive Cross-Chain Messages (Text/Data) using Native Coins for fees.
Native
BasicMessageSender.sol, BasicMessageReceiver.sol

Example 6
Send & Receive Cross-Chain Messages (Text/Data) using LINK Tokens for fees.
LINK
BasicMessageSender.sol, BasicMessageReceiver.sol

Example 7
Execute Received Message as a Function Call on the destination contract.
LINK or Native
FunctionCallSender.sol, FunctionCallReceiver.sol

Execution Workflow (General Steps):
    1. Deploy the Sender and Receiver contracts to their respective chains.
    2. Fund the Sender contract with LINK (or Native) to cover the CCIP fees.
    3. Execute the main transfer script (e.g., ccip-token-transfer task).
    4. Track the messageId on the CCIP Explorer.

5. Testing and Faucet
Testing

This project supports two types of tests:
Test Type
Description
Command (Example)
No Fork

Local tests using CCIPLocalSimulator.
npm run test:no-fork
Fork

Tests requiring a forked environment (e.g., Arbitrum Sepolia -> Ethereum Sepolia).
npm run test:fork

Faucet for Test Tokens
To ensure you never run out of tokens for testing, CCIP provides two ERC-20 test tokens (CCIP-BnM and CCIP-LnM) you can mint permissionlessly.
Use the dedicated faucet task to mint tokens to your wallet or contract:
Bash

# Example: Mint 1 CCIP-BnM token
npx hardhat faucet --receiver <RECEIVER_ADDRESS> --ccip-bnm <CCIP_BnM_ADDRESS>

6. Custom Token Pool Configuration

For users setting up custom tokens for cross-chain transfer, the following Hardhat tasks are available to streamline the process:
    1. deploy-token: Deploy a new ERC-20 token for CCIP.
    2. setup-burn-mint-pool: Set up a Burn-and-Mint token pool for your asset.
    3. setup-lock-release-pool: Set up a Lock-and-Release token pool.
    4. configure-pool: Configure rate limits and other parameters for an existing pool.
    5. send-ccip-tokens: Send tokens through a custom-configured pool.
