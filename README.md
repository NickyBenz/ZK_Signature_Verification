# ZK_Signature_Verification-
Verifying a signature using Zero-Knowledge Proofs (ZKPs) without revealing the underlying address 


# Aim 

The goal of this project is to verify that a signature by an Ethereum wallet address is whitelisted by a certain smart contract protocol without having to reveal any underlying details of the address

# Usage 

## Install Noir and Barattenburg 

- Install Noir 
```shell 
curl -L https://raw.githubusercontent.com/noir-lang/noirup/refs/heads/main/install | bash
noirup
```
- Install Barattenburg

```shell
curl -L https://raw.githubusercontent.com/AztecProtocol/aztec-packages/refs/heads/master/barretenberg/bbup/install | bash
bbup

```

## Compile Circuit 

Run 'nargo check' to validate syntax and build your Prover.toml 

Run 'nargo build' to compile the Noir code into an ACIR arithmetic circuit 

Run 'nargo execute' to generate a Prover.toml where the ZK witness will go 

## Generate Proof 

Run 'bb prove -b ./target/ZK_Simple_Circuit.json -w ./target/ZK_Simple_Circuit.gz -o ./target' to generate an off-chain proof -o ./target/verifier.sol 


## Verify Proof 

### Off-Chain Verification

Run 'bb write_vk ./target/ZK_Simple_Circuit.json -o ./target' to create the verification key

Run 'bb_verify -k ./target/vk -p ./target/proof ' to actually run the verification  

## On-Chain Verification

Run 'bb write_vk --oracle_hash keccack -b ./target/ZK_Simple_Circuit.json -o ./target' This will generate a verification key using keccak hashing, which is optimized for smart contract operations

Run 'bb write_solidity_verifier -k ./target/vk -p ./target/proof'  This will create a verifier smart contract for on-chain verification of Zero-Knowledge proofs. An example is already inside the repository 


