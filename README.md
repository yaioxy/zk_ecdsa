# Generate Proof and Verify it

1. Create Prover.toml to put the inputs
```
nargo check
```
2. Execute the circuit
```
nargo execute
```
3. Generate proof
```
nn prove -b ./target/simple_circuit.json -w ./target/simple_circuit.gz -o ./target
```
4. The verifier will run this to generate the verification key
```
bb write_vk -b ./target/simple_circuit.json -o ./target
```
5. Verify the proof
```
bb verify -k ./target/vk -p ./target/proof
```

# Generate Solidity Smart Contract
We can verify the input of the user & excpected address without revealing the inputs

1. Compile the circuit
```
nargo compile
```

2. Create verification key
```
bb write_vk --oracle_hash keccak -b ./target/zk_ecdsa.json -o ./target
```

3. Generate smart contract
```
bb write_solidity_verifier -k ./target/vk -o ./target/Verifier.sol
```
