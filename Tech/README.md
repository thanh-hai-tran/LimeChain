# Ethereum Tech Task

This directory provides a cross-chain messaging prototype named after "MyOApp" that allows connected smart contracts to communicate between different blockchain networks.

## Implementation

The implementation is based on LayerZero V2 and has the following directories and files:

- **contract** has contract *MyOApp.sol* that is based on LayerZero V2 to send and receive messages cross-chain.
- **deploy** has file *MyOApp.ts* to deploy contracts on testnets with Hardhat.
- **test** contains *MyOApp.test.ts* with test cases.
- *.env* requires a private key to check contracts on testnets.
- *hardhat.config.ts* contains configuration information for deployment with Hardhat. Currently, we use only Arbitrum, Base, and Optimism testnets. The information for Avalanche and Amoy testnets are provided as comments.
- *layerzero.config.ts* contains configuration information for LayerZero V2. This current setting allows instances on Arbitrum, Base, and Optimism testnets communicate each others.

## Security

By leveraging LayerZero V2, the prototype "MyOApp" supports the following mechanisms to enhance its security:
- Message origin proof uses relayer-submitted Merkle proofs.
- Sender authenticity allows only trusted peers, which are updated via function *setPeer*, to send messages.
- Global unique identifier (*GUID*) ensure messages can be tracked across the network and prevent replay attacks. This identifier is generated for each LayerZero message that combines the message's nonce, source chain, destination chain, and participating contracts. GUIDs ensure messages can be tracked across the network and prevent replay attacks.

## Trade-offs & optimizations
While this current approach makes communication on different chains effectively in many cases, it has the following trade-offs:
- This prototype assumes that LayerZero's default Oracle and Relayer, which are currently operated by LayerZero Labs, is correct and reliable.
- Incorrect setup, e.g., misconfigured trusted peers, can lead to message hijacking or loss.
- Decentralized Verifier Networks (DVNs) make verifiers more fault-tolerant but require more computaion and resources.

Some alternative solutions for LayerZero are Axelar, Wormhole, or Hyperlane.

Moreover, if we want to focus only on tokens, we should consider bridges. 
