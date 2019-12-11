# TSSKit: Threshold Signature Scheme Toolkit
![](https://img.shields.io/badge/Funds-Binance%20Labs-yellow.svg)
![](https://img.shields.io/badge/Grants-Gitcoin-green.svg)
![](https://img.shields.io/badge/Build-Turing%20Chain-red.svg)

![](https://imgur.com/iJbwYW6.png)


## Table of Contents 
  - [Description](#Description)
  - [Types of Schemes](#Types-of-Schemes)
  - [Options](#Options)
  - [Conceptual Comparisons across Schemes](#Conceptual-Comparisons-across-Schemes)
  - [Multi Signature vs Threshold Signature](#Multi-Signature-vs-Threshold-Signature)
  - [Codebases](#Codebases)
    - [ECDSA](#ECDSA)
    - [Schnorr](#Schnorr)
    - [Ed25519](#Ed25519)
    - [BLS](#BLS)
  - [References](#References)
  
## Description
TSSKit automatically selects the appropriate Threshold Signature Scheme based on a set of options required by the secret sharing needs of each application.   This comprehensive list of options includes private key splitting, multisig detection, HD derivation, signer privacy, and signature size, etc.

TSSKit also generates a set of ready-to-use codebase/scripts that are optimized based on a set of specified parameters.

> Welcome to create any number of pull requests to contribute more codebases that we've missed. BUIDL!

**Active curators: [yhuag](https://github.com/yhuag) and [tina1998612](https://github.com/tina1998612)**

**Active reviewers: [ChenPoWei](https://github.com/ChenPoWei)**

## Types of Schemes
- Shamir's Secret Sharing (SSS)
- Threshold ECDSA
- Threshold Ed25519
- Schnorr Signatures
- BLS Signatures

## Options
| Option                    | Choice                    |
| ------------------------- | ------------------------- |
| Private Key Splitting     | True / False              |
| Multi-signature Detection | True / False              |
| HD Derivation             | True / False              |
| Weight                    | True / False              |
| Signer Privacy            | True / False              |
| Signature Size            | Linear Growth / Constant  |
| Key Generation Time       | Linear Growth / Constant  |
| Key Generation Round      | Value                     |
| Key Generation Role       | Single Party / DKG Scheme |
| Verification Time         | Strict / Relax            |
| Signing Time              | Strict / Relax            |
| Signing Round             | Value                     |
| Curve                     | Curve Choice              |

> Free to create pull request to add more

## Conceptual Comparisons across Schemes

<table>
  <tr>
    <td></td>
    <td>t-ECDSA</td>
    <td>t-Schnorr</td>
    <td>Ed25519</td>
    <td>BLS</td>
  </tr>
  <tr>
    <td><b>Variants</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Has non-threshold variant</td>
    <td>✔︎</td>
    <td>✔︎</td>
    <td>✔︎

</td>
    <td>✘
</td>
  </tr>
  <tr>
    <td><b>Curve</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Curve Family</td>
    <td>Elliptic</td>
    <td>Elliptic</td>
    <td>Twisted Edwards</td>
    <td>Pairing-friendly</td>
  </tr>
  <tr>
    <td><b>Signature</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Size (bytes)</td>
    <td>71 - 75</td>
    <td>64</td>
    <td>64</td>
    <td>33</td>
  </tr>
  <tr>
    <td>Aggregation</td>
    <td>X</td>
    <td>Entire multi-sig</td>
    <td>Entire multi-sig (variant)</td>
    <td>Entire block</td>
  </tr>
  <tr>
    <td>Format</td>
    <td>Pair</td>
    <td>Pair</td>
    <td>Pair</td>
    <td>Single Curve Point</td>
  </tr>
  <tr>
    <td>Multisignature Differentiable</td>
    <td>✔︎</td>
    <td>✘</td>
    <td>✘</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td><b>Signing</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Time Complexity</td>
    <td>High</td>
    <td>Medium</td>
    <td>Low</td>
    <td>Low</td>
  </tr>
  <tr>
    <td>Interaction Rounds</td>
    <td>Multiple</td>
    <td>Two</td>
    <td>Three</td>
    <td>✘</td>
  </tr>
  <tr>
    <td><b>Verifying</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Verification Targets</td>
    <td>Separately</td>
    <td>Aggregated</td>
    <td>Batch / Single</td>
    <td>Aggregated</td>
  </tr>
  <tr>
    <td>Time Complexity</td>
    <td>Medium</td>
    <td>Low</td>
    <td>Low</td>
    <td>High</td>
  </tr>
  <tr>
    <td><b>Block</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Block Capacity Usage</td>
    <td>Large </td>
    <td>Medium </td>
    <td>Medium</td>
    <td>Small </td>
  </tr>
  <tr>
    <td>Block Content</td>
    <td>Signature + Public Key + Data</td>
    <td>Several Combined Signatures + Public Key + Data</td>
    <td>Several Combined Signatures + Public Key + Data</td>
    <td>One Aggregated Signature + Public Key + Data</td>
  </tr>
  <tr>
    <td><b>Randomness</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Random Number Generator (k)</td>
    <td>Deterministic</td>
    <td>Strictly Dependent</td>
    <td>Deterministic</td>
    <td>Not Required</td>
  </tr>
  <tr>
    <td>New Randomness Consumption</td>
    <td>Key Generation, Signing</td>
    <td>Key Generation, Signing</td>
    <td>Key Generation</td>
    <td>Not Required</td>
  </tr>
  <tr>
    <td><b>Setup</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Key Generation</td>
    <td>DKG</td>
    <td>DKG</td>
    <td>DKG</td>
    <td>Membership</td>
  </tr>
  <tr>
    <td>Key Storage</td>
    <td>N/A</td>
    <td>Merkle Tree (Verifying)</td>
    <td>N/A</td>
    <td>Pre-generate all the keys (Signing)</td>
  </tr>
  <tr>
    <td>Space Complexity</td>
    <td>Low</td>
    <td>High</td>
    <td>Low</td>
    <td>Positively correlated with the number of signing cycles</td>
  </tr>
  <tr>
    <td>Time Complexity</td>
    <td>High </td>
    <td>Medium</td>
    <td>Low</td>
    <td>High</td>
  </tr>
  <tr>
    <td>Time Bottleneck</td>
    <td>The curve used for generating key public / private pairs</td>
    <td>1. The curve used for generating key public / private pairs
1. n and m for merkle tree </td>
    <td>Random Number Generator</td>
    <td>Takes time to generate membership keys</td>
  </tr>
  <tr>
    <td><b>Security</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Hash Collision Resilience</td>
    <td>Low</td>
    <td>High</td>
    <td>High</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>Side-channel Attack Resilience</td>
    <td>Low</td>
    <td>High (variant)</td>
    <td>High</td>
    <td>High</td>
  </tr>
  <tr>
    <td>Other Possible Attacks</td>
    <td>Secp112r1 Leakage Attacks,
Weak RNG Attacks</td>
    <td>Rogue Key Attacks</td>
    <td>Single Fault Attacks</td>
    <td>MOV Attacks, Rogue Key Attacks</td>
  </tr>
  <tr>
    <td><b>Hashing</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Hash Output</td>
    <td>Number</td>
    <td>Number</td>
    <td>Number</td>
    <td>Curve Point</td>
  </tr>
  <tr>
    <td><b>Privacy</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Public Key</td>
    <td>Revealed</td>
    <td>Hidden</td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
</table>

## Multi Signature vs Threshold Signature
|                                                                                                      | Multi-sig                                                                                                  | Threshold-sig                                                      |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Relationship between (number of signers) and  (signature length, generation time, verification time) | Scales linearly                                                                                            | Independent                                                        |
| Reveal the identities of signers                                                                     | Yes                                                                                                        | No                                                                 |
| Signature verification                                                                               | Use all public keys                                                                                        | Use a unique fixed public key                                      |
| Can do m-out-of-n signing                                                                            | Yes                                                                                                        | Yes                                                                |
| Signature is composed of                                                                             | Concatenation of ( description of the subgroup + regular signatures computed by each member’s secret key ) | Regular signatures computed by all members' aggregated private key |
  

## Codebases
## ECDSA
#### Javascript
1. Bitchain (npm / non-threshold):  https://github.com/bitchan/eccrypto
2. Elliptic (npm / non-threshold): https://www.npmjs.com/package/elliptic

#### C++
1. kmackay (non threshold): https://github.com/kmackay/micro-ecc

#### C
1. esxgx (non threshold): https://github.com/esxgx/easy-ecc
2. freifunk-gluon (non-threshold): https://github.com/freifunk-gluon/ecdsautils

#### Rust
1. KZen: https://github.com/KZen-networks/multi-party-ecdsa
2. Rust-bitcoin (non-threshold): https://github.com/rust-bitcoin/rust-secp256k1/

#### Go
1. bftkv: https://github.com/yahoo/bftkv/blob/master/crypto/threshold/ecdsa/ecdsa.go

#### Java
1. TwoFactorBtc: https://github.com/citp/TwoFactorBtcWallet/tree/master/EcdsaTwoPartyThresholdSignature/src/main/java/threshold/mr04

#### Python
1. Fernandolobato: https://github.com/fernandolobato/ecc_verifiable_threshold_cryptosystem

2. AntonKueltz: https://github.com/AntonKueltz/fastecdsa

3. warner (non threshold): https://github.com/warner/python-ecdsa

4. SolCrypto (non-threshold): https://github.com/HarryR/solcrypto

#### Swift
1. Sajjon (non-threshold): https://github.com/Sajjon/EllipticCurveKit

## Schnorr
#### Javascript
1. NPM: https://github.com/guggero/bip-schnorr

2. Bcoin: https://github.com/bcoin-org/schnorr

3. guggero (non-threshold): https://github.com/guggero/bip-schnorr

#### C

1. openssh: https://github.com/metacloud/openssh/blob/master/schnorr.c

2. metalicjames: https://github.com/metalicjames/cschnorr

3. OkCupid: https://github.com/OkCupid/sfslite/blob/master/crypt/schnorr.C

#### Rust
1. KZen: https://github.com/KZen-networks/multi-party-schnorr

2. W3f: https://github.com/w3f/schnorrkel

#### Go
1. hbakhtiyor (non-threshold): https://github.com/hbakhtiyor/schnorr

#### Java
1. DimonK95: https://github.com/DimonK95/schnorr-signature

#### Python
1. Yuntai: https://github.com/yuntai/schnorr-examples

2. Vihu: https://github.com/vihu/schnorr-python/blob/master/naive.py

3. SolCrypto (non-threshold): https://github.com/HarryR/solcrypto

## Ed25519
#### Javascript
1. NPM: https://github.com/dazoe/ed25519

2. Substack-Supercop-ref10: https://github.com/substack/ed25519-supercop

3. Ed25519 (npm): https://www.npmjs.com/package/ed25519

4. Ed25519-Supercop (npm): https://www.npmjs.com/package/ed25519-supercop

5. Ed25519-hap (npm): https://www.npmjs.com/package/ed25519-hap

6. Ed25519-hd-key: https://www.npmjs.com/package/ed25519-hd-key

7. Types (npm): https://www.npmjs.com/package/@types/ed25519

#### C++
1. Floodyberry: https://github.com/floodyberry/ed25519-donna

2. MIT DCI: https://github.com/mit-dci/CryptoKernel

#### C
1. Orlp: https://github.com/orlp/ed25519

#### Rust
1. Dalek: https://github.com/dalek-cryptography/ed25519-dalek

#### Go
1. Dcrd: https://github.com/decred/dcrd/blob/master/dcrec/edwards/ecdsa.go

2. Agl: https://github.com/agl/ed25519/blob/master/edwards25519/edwards25519.go

3. Golang: https://github.com/golang/crypto/tree/master/ed25519

#### Java
1. Crypto-rb: https://github.com/crypto-rb/ed25519

2. Str4d: https://github.com/str4d/ed25519-java

#### Python
1. warner (non threshold): https://github.com/warner/python-ed25519

2. official: https://ed25519.cr.yp.to/python/ed25519.py

3. official pip: https://pypi.org/project/ed25519/

## BLS
#### Javascript
1. Difnity (npm): https://github.com/dfinity/js-bls-lib

2. Kfichter: https://github.com/kfichter/solidity-bls

3. bls-signatures (npm): https://www.npmjs.com/package/bls-signatures

#### TypeScript
1. ChainSafe: https://github.com/ChainSafe/bls-js

#### C++
1. Herumi: https://github.com/herumi/bls

2. Leishman: https://github.com/leishman/bls_lib

3. Skale: https://github.com/skalenetwork/libBLS

#### C
1. Chia Network: https://github.com/Chia-Network/bls-signatures

#### Rust
1. Filecoin: https://github.com/filecoin-project/bls-signatures

2. Lovesh: https://github.com/lovesh/signature-schemes

3. Str4d: https://github.com/str4d/bls

#### Go
1. Enzoh: https://github.com/enzoh/go-bls

2. Prysmaticlabs: https://github.com/prysmaticlabs/go-bls

#### Python
1. Asonnino: https://github.com/asonnino/bls

2. pip: https://pypi.org/project/python-bls/

3. bls-lib doc: https://bls-lib.readthedocs.io/en/latest/

## References
1. Alternative Signatures Schemes: [https://blockchainatberkeley.blog/alternative-signatures-schemes-14a563d9d562](https://blockchainatberkeley.blog/alternative-signatures-schemes-14a563d9d562)  

2. Multisig vs SSS vs Threshold signature (with graph illustration): [https://www.kzencorp.com/post/threshold-signatures-private-key-the-next-generation](https://www.kzencorp.com/post/threshold-signatures-private-key-the-next-generation)  

3. How Schnorr signatures may improve Bitcoin: [https://medium.com/cryptoadvance/how-schnorr-signatures-may-improve-bitcoin-91655bcb4744](https://medium.com/cryptoadvance/how-schnorr-signatures-may-improve-bitcoin-91655bcb4744)

4. BLS signatures: better than Schnorr: [https://medium.com/cryptoadvance/bls-signatures-better-than-schnorr-5a7fe30ea716](https://medium.com/cryptoadvance/bls-signatures-better-than-schnorr-5a7fe30ea716)

5. ECDSA is not that bad: two-party signing without Schnorr or BLS: [https://medium.com/cryptoadvance/ecdsa-is-not-that-bad-two-party-signing-without-schnorr-or-bls-1941806ec36f](https://medium.com/cryptoadvance/ecdsa-is-not-that-bad-two-party-signing-without-schnorr-or-bls-1941806ec36f) 

6. Generator Point: [https://crypto.stackexchange.com/questions/53321/what-are-the-coordinates-of-a-generator-point](https://crypto.stackexchange.com/questions/53321/what-are-the-coordinates-of-a-generator-point)

7. Elliptic Curve Cryptography: [https://eng.paxos.com/blockchain-101-elliptic-curve-cryptography](https://eng.paxos.com/blockchain-101-elliptic-curve-cryptography)

8. Why Schnorr signatures will help solve 2 of Bitcoin’s biggest problems today: [https://medium.com/@SDWouters/why-schnorr-signatures-will-help-solve-2-of-bitcoins-biggest-problems-today-9b7718e7861c](https://medium.com/@SDWouters/why-schnorr-signatures-will-help-solve-2-of-bitcoins-biggest-problems-today-9b7718e7861c)

9. Schnorr Signatures & The Inevitability of Privacy in Bitcoin: [https://medium.com/digitalassetresearch/schnorr-signatures-the-inevitability-of-privacy-in-bitcoin-b2f45a1f7287](https://medium.com/digitalassetresearch/schnorr-signatures-the-inevitability-of-privacy-in-bitcoin-b2f45a1f7287)

10. ECDSA: [https://blog.cloudflare.com/ecdsa-the-digital-signature-algorithm-of-a-better-internet/](https://blog.cloudflare.com/ecdsa-the-digital-signature-algorithm-of-a-better-internet/) 

11. ed25519: [https://ed25519.cr.yp.to/](https://ed25519.cr.yp.to/) 

12. schnorr: [https://github.com/WebOfTrustInfo/rwot1-sf/blob/master/topics-and-advance-readings/Schnorr-Signatures--An-Overview.md](https://github.com/WebOfTrustInfo/rwot1-sf/blob/master/topics-and-advance-readings/Schnorr-Signatures--An-Overview.md) 

13. choice of curve affects key size: [https://stackoverflow.com/questions/6665353/is-there-a-standardized-fixed-length-encoding-for-ec-public-keys](https://stackoverflow.com/questions/6665353/is-there-a-standardized-fixed-length-encoding-for-ec-public-keys)  

14. SafeCurves: [http://safecurves.cr.yp.to/ladder.html](http://safecurves.cr.yp.to/ladder.html) 

15. Curve Comparisons: [http://safecurves.cr.yp.to/index.html](http://safecurves.cr.yp.to/index.html)

16. min key size recommendation website: [https://www.keylength.com/en/4/](https://www.keylength.com/en/4/) 

17. Why are key lengths in asymmetric algorithms typically longer than key lengths in symmetric algorithms?: [https://crypto.stackexchange.com/questions/46852/why-are-key-lengths-in-asymmetric-algorithms-typically-longer-than-key-lengths-i](https://crypto.stackexchange.com/questions/46852/why-are-key-lengths-in-asymmetric-algorithms-typically-longer-than-key-lengths-i) 

18. Elliptic curve Schnorr-based signatures in Bitcoin: [https://diyhpl.us/wiki/transcripts/scalingbitcoin/milan/schnorr-signatures/](https://diyhpl.us/wiki/transcripts/scalingbitcoin/milan/schnorr-signatures/)

19. Ed25519 Signature 2018: [https://w3c-dvcg.github.io/lds-ed25519-2018/](https://w3c-dvcg.github.io/lds-ed25519-2018/)

20. Aggregated Ed25519 Signature: [https://github.com/KZen-networks/multi-party-eddsa/wiki/Aggregated-Ed25519-Signatures#aggregated-ed25519-signature](https://github.com/KZen-networks/multi-party-eddsa/wiki/Aggregated-Ed25519-Signatures#aggregated-ed25519-signature)

21. Schnorr signatures: [https://diyhpl.us/wiki/transcripts/scalingbitcoin/milan/schnorr-signatures/](https://diyhpl.us/wiki/transcripts/scalingbitcoin/milan/schnorr-signatures/)

22. BLS: Is it really that slow?: [https://blog.dash.org/bls-is-it-really-that-slow-4ca8c1fcd38e](https://blog.dash.org/bls-is-it-really-that-slow-4ca8c1fcd38e)

23. Hash Function Requirementsfor Schnorr Signatures: [http://www.neven.org/papers/schnorr.pdf](http://www.neven.org/papers/schnorr.pdf)

24. A conversation with Dan Boneh: [https://diyhpl.us/wiki/transcripts/2016-july-bitcoin-developers-miners-meeting/dan-boneh/](https://diyhpl.us/wiki/transcripts/2016-july-bitcoin-developers-miners-meeting/dan-boneh/)

25. ecdsa attack: [https://crypto.stackexchange.com/questions/55876/is-there-any-ecdsa-attack-if-i-have-millions-of-signatures](https://crypto.stackexchange.com/questions/55876/is-there-any-ecdsa-attack-if-i-have-millions-of-signatures) 

26. A Leakage-Resilient Pairing-Based Variant of the Schnorr Signature Scheme: [https://link.springer.com/chapter/10.1007/978-3-642-45239-0_11](https://link.springer.com/chapter/10.1007/978-3-642-45239-0_11)

27. Bitcoin Stackexchange: [https://bitcoin.stackexchange.com/questions/50836/multi-signature-public-key-validation](https://bitcoin.stackexchange.com/questions/50836/multi-signature-public-key-validation) 

28. Fast Multiparty Threshold ECDSA with Fast Trustless Setup: [https://www.iacr.org/archive/pkc2003/25670031/25670031.pdf](https://www.iacr.org/archive/pkc2003/25670031/25670031.pdf) 
