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

## Contributions

### 2000 Tx Circuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [circuit-2000-32-256-64_hez1_0000.zkey]()     | |
| 0001_jordi | [circuit-2000-32-256-64_hez1_0001.zkey]()     | [Jordi](https://keybase.io/jbaylina)  | `00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`<br>`00000000 00000000`|

### 376 Tx Circuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [circuit-376-32-256-64_hez1_0000.zkey]()     | |
| 0001_jordi | [circuit-376-32-256-64_hez1_0001.zkey]()     | [Jordi](https://keybase.io/jbaylina)  | `f69ea0f7 251ed117`<br>`6d3e2b05 e1e814c4`<br>`fc7d764f 83a5f00c`<br>`c07c0ee1 0140cb46`<br>`9211ab52 3bc8ab0d`<br>`2ec0e6ee 28a310fd`<br>`6f776e24 a270e83f`<br>`c9a1777f 6e0680ea`|


### WithdrawCircuit

| Atestation<br>&nbsp; | Contribution File<br>&nbsp; | Contributor<br>&nbsp; | Contribution Hash &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; <br> &nbsp; |
|:-----|:------------ |:-----|:--------------------------------------|
| 0000_initial | [withdraw_hez1_0000.zkey]()     | |
| 0001_jordi | [withdraw_hez1_0001.zkey]()     | [Jordi](https://keybase.io/jbaylina)  |     `25b83ba8 1db23b31`<br>`ddd54f03 cfa7723c`<br>`2229320c a075b8fc`<br>`8d04b186 acd140db`<br>`43b1d398 266861f6`<br>`2e82da13 6bf8bf06`<br>`77512609 ab2cb254`<br>`e3d3e8b4 448299ad`|


## How to contribute

Contact #trusted-setup-phase2-ceremony channel in the Hermez discord to be added into the queue and coordinate the details.

You can also reach us in the [Hermez Telegram group](https://t.me/hermez_network).

## Requirements

A machine with 4 cores and 16Gb would do the work, but we recomend a bigger machine to process the ceremony faster.

In this tutorial I'll describe all the steps required to run them in a new m5a.4xlarge aws instance with ubuntu 20.04.  But this is just for reference. It's better if you run your own hardware.

### Preparation of the machine.

You can use any machine to run the ceremony. The important part of the ceremony is that the toxic value is not leaked and it's deleted after the completion of the ceremony.

This toxic value is in the memory while the ceremony is running. This toxic value is not displayed any where, and it's recomended to restart the machine after the ceremony is completed to be sure this toxic value is not accessible any more.

You can check the [phase1 perpetual powers of tau ceremony](https://github.com/weijiekoh/perpetualpowersoftau) used by Hermez for geting ideas.

Once we start
````
````

You will need node version at least v14. For reference we are using v14.8.0

Install snarkjs:

````bash
npm install snarkjs
````

At the begining of the contribution you will receive 3 files:

* `circuit-2000-32-256-64_hez1_xxxx.zkey`
* `circuit-376-32-256-64_hez1_xxxx.zkey`
* `withdraw_hez1_xxxx.zkey`

Where `xxxx` is the contribution of the last participant.

Take note of the blake2b of the imputs and check with the ceremony coordinator the integrity of the files:
````bash
b2sum circuit-2000-32-256-64_hez1_xxxx.zkey
b2sum circuit-375-32-256-64_hez1_xxxx.zkey
b2sum withdraw_hez1_xxxx.zkey
````

To run the ceremony you need to run:

````bash
snarkjs zkey contribute circuit-2000-32-256-64_hez1_xxxx.zkey circuit-2000-32-256-64_hez1_yyyy.zkey -v -n="Your name"
````

"Your name" is added in the file for reference. This is important because this name will be displayed with the contribution hash when all the contributions are listed in the fine zkey file.

Substitute also `yyyy` by the actual contrubution.  This should be `xxxx` + 1.

Write down the Circuit Hash and The Contribution Hash printed at the end.

The circuit hash should be:

````
````

Do the same for the other two circuits:

````
snarkjs zkey contribute circuit-376-32-256-64_hez1_xxxx.zkey circuit-376-32-256-64_hez1_yyyy.zkey -v -n="Your name"
snarkjs zkey contribute withdraw_hez1_xxxx.zkey withdraw_hez1_yyyy.zkey -v -n="Your name"
````

The circuit hash for `circuit-376-32-256-64` should be:

````
d357a1ec f80bbc0e ba06ae34 4a40c688
79026153 c5a1c550 28b6ac02 3789d26c
b3c59f9b eb74cd2e 13f7ce35 7f2b18fd
08dc9f7f 1abf46f6 98f6a5c4 a8b2ce98
````

And the circuit of the withdraw circuit should be:

````
ec15023b 4b03e104 a8b8f620 e48b6f8a
f6231eeb d3a3e47c c7745379 34b16062
301a0ad3 91d56c7e cf98b8d3 28f231f5
42f67e89 893e2b21 277e7019 55020b8c
````

Write down the contribution hash for both circuits.

Now you can checksum your contributions by running:

````
b2sum circuit-2000-32-256-64_hez1_yyyy.zkey
b2sum circuit-375-32-256-64_hez1_yyyy.zkey
b2sum withdraw_hez1_yyyy.zkey
````

With this, you will have all the information to fill the atestation template.

Create a copy of the [template file]() with name `yyyy_YourName_attestation.txt`

Fill all the fields of the template.

Sign the template with a PGP key.

and generate a signed atestation with name:
`yyyy_YourName_attestation_signed.txt`


Send the 3 responses plus the signed attestation to the coordinator.

You will be asked to do so by first create a ssh-key if you don't have it.

````
ssh-keygen
````

Send the public key to the ceremony coordinator.
You can see your public key by typing:

````
cat ~/.ssh/id_rsa.pub
````

Once the ceremony coordinator authorizes your key, you can upload the generated files and the signed atestation by doing:

````
sftp YouName@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put circuit-2000-32-256-64_hez1_yyyy.zkey'
sftp YouName@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put circuit-376-32-256-64_hez1_yyyy.zkey'
sftp YouName@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put withdraw_hez1_yyyy.zkey'
sftp YouName@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put yyyy_YourName_attestation_signed.txt'
````

Send also your PGP Key or a link to yout PGP keybase to the coordinator.


## Verification of the ceremony

In order to verify the circuit, you will need a machine with tons of memory.

For reference, the one we are using is a machine with 16cores and 512Gb of RAM.

We will give instructions for a x1e.8xlarge aws instance.



#### Tweek the OS to accept high amount of memory.

#### Compile a patched version of node

#### Compile the circuit

#### Optimize the circuit

#### Verify the zkey file.

#### Verify the attestations.

#### Make a public post.



