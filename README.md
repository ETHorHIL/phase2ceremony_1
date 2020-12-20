# Hermez Network First Phase2 Trusted Setup Ceremony.

This repository contains the transcript of the Phase2 Ceremony.

This ceremony runs the trusted setup for 3 circuits:

* **circuit_circuit-2000-32-256-64**
* **circuit_circuit-376-32-256-64**
* **withdraw**

The first two circuits are the validation circuits for 2000Tx and 376 Txs.  The third circuit is the one used in the rollup exits.

See [Hermez Documentation](https://docs.hermez.io/#/) for fore information of how the rollup works.

The Circom circuits can be found in [circuits](https://github.com/hermeznetwork/circuits).

For this ceremony we used the tag `phase2ceremony_1` with commit value  `16f791efd259f2b158bc48b1911ab94ac1e53d36`

For contributing to the ceremony see: [CONTRIBUTE.md](CONTRIBUTE.md)

For verifying the ceremony see: [VERIFY.md](VERIFY.md)

## Contributions

### 2000 Tx Circuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [circuit-2000-32-256-64_hez1_0000.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-2000-32-256-64_hez1_0000.zkey)     | |
| [0001_jordi](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0001_jordi) | [circuit-2000-32-256-64_hez1_0001.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-2000-32-256-64_hez1_0001.zkey)     | [jbaylina](https://keybase.io/jbaylina)  | `a8393a38 b4f3607a`<br>`ca08a629 92e1ac25`<br>`c4274c2f 7fd1828f`<br>`f93c655d 31d7e4cf`<br>`39731c5e 2e9be49b`<br>`c46580a4 4ab291a6`<br>`08ed8beb 1a1e3215`<br>`a826485e 0ea06b38` |
| [0002_eduadiez](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0002_eduadiez) | [circuit-2000-32-256-64_hez1_0002.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-2000-32-256-64_hez1_0002.zkey)     | [eduadiez](https://keybase.io/eduadiez)  | `295e7ada 0c4bb771`<br>`cb792700 d4a81730`<br>`95350191 fe55d1ad`<br>`854d9abc 4991ccd6`<br>`9335269a c886f48a`<br>`5e28efef f6dc25c3`<br>`f1527ca5 42f5f32d`<br>`5b756870 b84f30b7` |

### 376 Tx Circuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [circuit-376-32-256-64_hez1_0000.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-376-32-256-64_hez1_0000.zkey)     | |
| [0001_jordi](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0001_jordi) | [circuit-376-32-256-64_hez1_0001.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-376-32-256-64_hez1_0001.zkey)     | [Jordi](https://keybase.io/jbaylina)  | `f69ea0f7 251ed117`<br>`6d3e2b05 e1e814c4`<br>`fc7d764f 83a5f00c`<br>`c07c0ee1 0140cb46`<br>`9211ab52 3bc8ab0d`<br>`2ec0e6ee 28a310fd`<br>`6f776e24 a270e83f`<br>`c9a1777f 6e0680ea`|
| [0002_eduadiez](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0002_eduadiez) | [circuit-376-32-256-64_hez1_0002.zkey](https://hermez.s3-eu-west-1.amazonaws.com/circuit-376-32-256-64_hez1_0002.zkey)     | [eduadiez](https://keybase.io/eduadiez)  | `7a7f023f 7a6d0d25`<br>`9dd6b907 4d79f238`<br>`cf9ebefd b88e5e57`<br>`ec50e58d 5693d627`<br>`bed74f02 37084cbd`<br>`29758bf8 51c2a96d`<br>`2291a5e1 d658c217`<br>`4a89cea7 a840aca5` |

### WithdrawCircuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; <br> &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [withdraw_hez1_0000.zkey](https://hermez.s3-eu-west-1.amazonaws.com/withdraw_hez1_0000.zkey)     | |
| [0001_jordi](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0001_jordi) | [withdraw_hez1_0001.zkey](https://hermez.s3-eu-west-1.amazonaws.com/withdraw_hez1_0001.zkey)     | [Jordi](https://keybase.io/jbaylina)  |     `25b83ba8 1db23b31`<br>`ddd54f03 cfa7723c`<br>`2229320c a075b8fc`<br>`8d04b186 acd140db`<br>`43b1d398 266861f6`<br>`2e82da13 6bf8bf06`<br>`77512609 ab2cb254`<br>`e3d3e8b4 448299ad`|
| [0002_eduadiez](https://github.com/hermeznetwork/phase2ceremony_1/tree/main/0002_eduadiez) | [withdraw_hez1_0002.zkey](https://hermez.s3-eu-west-1.amazonaws.com/withdraw_hez1_0002.zkey)     | [eduadiez](https://keybase.io/eduadiez)  | `4ea15ed5 363c2561`<br>`305acf41 a8fa52a6`<br>`8820ba40 3e960467`<br>`1d386b07 195de3dd`<br>`01d59ab4 49e72d5c`<br>`3c429ec0 e707fb4c`<br>`9b8d9287 9492a299`<br>`ea36039f b980e7fe` |

