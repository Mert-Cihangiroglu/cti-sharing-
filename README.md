# Project Title

CTI SHARING Using Swarm learning and zero knowledge proofs.

## Table of Contents

- [Setup](#setup)
- [Federated Learning Scheme](#federated-learning-scheme)
    - [Coordinator Contract](#coordinator-contract)
    - [Organizations (Learning Nodes)](#organizations-learning-nodes)
    - [Organizations (Validators)](#organizations-validators)
    - [Aggregator](#aggregator)
- [Circuit Generation](#circuit-generation)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Setup

The setup is primarily handled by the system generator. Follow these steps to prepare your environment for the federated learning scheme.

### Deploy the Coordinator Contract

1. **Deploy the `CoordinatorContract` contract.**
    - This contract orchestrates the entire process.

2. **Whitelist Organizations**
    - Organizations must provide their public key (also known as blockchain wallet address) to be whitelisted.
    - Only submissions from whitelisted addresses are accepted by `CoordinatorContract`. Submissions include Individual Verifier Smart Contract Address, IPFS Model Hash, and Gradient Updates.

### Start Learning

- With `CoordinatorContract` set up, initiate the federated learning process by calling the public `startLearning` function.
    - **Input 1**: Address of the Aggregator.
    - **Input 2**: List of whitelisted organizations' addresses.
- This initiates a unique swarm learning scheme ID.

## Federated Learning Scheme

### Coordinator Contract

- The contract is public and permissionless, enabling any organization to start the learning process.
- Organizations query the `isReady` function to check readiness. If true, they proceed to download required data from IPFS using `srsIPFSHash` and `globalModelIPFSHash` functions.

### Organizations (Learning Nodes)

1. **Start PyTorch Training**: Begin training your model using PyTorch.
2. **Model Conversion**: Convert the PyTorch model to ONNX format.
3. **Circuit Generation**: Follow the circuit generation steps to create and deploy the `verify.sol` file.
4. **Submission**: Submit the smart contract address of `verify.sol` to `CoordinatorContract` and start querying the `ValidatorList` function.

### Organizations (Validators)

- Validators are selected by the `CoordinatorContract` after all learning nodes submit their verifier smart contracts.
- Validators download models, run tests, generate proofs using ZKML library, and publish the results.

### Aggregator

- Any organization can assume the role of an Aggregator, with all aggregation files being publicly verifiable.

## Circuit Generation

Follow these steps to generate and deploy verifier contracts:

1. **Prepare Environment**:
    - Install Forge: [Installation Guide](https://book.getfoundry.sh/getting-started/installation)
    - Install required libraries: `pip install -r requirements.txt`

2. **Local Blockchain**:
    - Start a local blockchain with `anvil`.

3. **Deploy Coordinator Contract**:
    - Use `forge create <ContractName> --interactive` and follow the prompts.

4. **Generate Verifier Contract**:
    - Ensure you have `network.onnx`, `input.json`, and the SRS file ready.
    - Follow the provided commands to generate settings, compile the circuit, and deploy the Solidity verifier contract.

## Requirements

List of software and library requirements.

## Installation

Steps to install the project.

## Usage

Instructions on how to use the system once set up.

## Contributing

Guidelines for contributing to the project.

## License

License information.
