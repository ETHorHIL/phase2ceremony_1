# Hermez Network First Phase2 Trusted setup ceremony.

This repository contains the transcript of the phase2 ceremony.

This ceremony runs the trusted setup for 3 circuit:

* **circuit_circuit-2000-32-256-64**
* **circuit_circuit-376-32-256-64**
* **withdraw**

The first two circuits are the validation circuits for 2000Tx and 376 Txs.  The third circuit is the one used in the rollup exits.

See [Hermez Documentation](https://docs.hermez.io/#/) for fore information of how the rollup works.

The circom circuits can be found in [circuits](https://github.com/hermeznetwork/circuits).

For this ceremony we used the tag `phase2ceremony_1` with commit value  `16f791efd259f2b158bc48b1911ab94ac1e53d36`

For contributing to the ceremony see: [CONTRIBUTE.md]()
For verifying the ceremony see: [VERIFY.md]()

## Contributions

### 2000 Tx Circuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [circuit-2000-32-256-64_hez1_0000.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-2000-32-256-64_hez1_0000.zkey)     | |
| [0001_jordi](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0001_jordi) | [circuit-2000-32-256-64_hez1_0001.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-2000-32-256-64_hez1_0001.zkey)     | [Jordi](https://keybase.io/jbaylina)  | `00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`|

### 376 Tx Circuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [circuit-376-32-256-64_hez1_0000.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-376-32-256-64_hez1_0000.zkey)     | |
| [0001_jordi](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0001_jordi) | [circuit-376-32-256-64_hez1_0001.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-376-32-256-64_hez1_0001.zkey)     | [Jordi](https://keybase.io/jbaylina)  | `f69ea0f7 251ed117`<br>`6d3e2b05 e1e814c4`<br>`fc7d764f 83a5f00c`<br>`c07c0ee1 0140cb46`<br>`9211ab52 3bc8ab0d`<br>`2ec0e6ee 28a310fd`<br>`6f776e24 a270e83f`<br>`c9a1777f 6e0680ea`|


### WithdrawCircuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; <br> &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [withdraw_hez1_0000.zkey](https://hermez.s3-eu-west-1.amazonaws.com/withdraw_hez1_0000.zkey)     | |
| [0001_jordi](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0001_jordi) | [withdraw_hez1_0001.zkey](https://hermez.s3-eu-west-1.amazonaws.com/withdraw_hez1_0001.zkey)     | [Jordi](https://keybase.io/jbaylina)  |     `25b83ba8 1db23b31`<br>`ddd54f03 cfa7723c`<br>`2229320c a075b8fc`<br>`8d04b186 acd140db`<br>`43b1d398 266861f6`<br>`2e82da13 6bf8bf06`<br>`77512609 ab2cb254`<br>`e3d3e8b4 448299ad`|

