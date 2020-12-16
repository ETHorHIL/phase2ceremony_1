
# How to contribute

Contact #trusted-setup-phase2-ceremony channel in the Hermez discord to be added into the queue and coordinate the details.

You can also reach us in the [Hermez Telegram group](https://t.me/hermez_network).

## Requirements

A machine with 4 cores and 16Gb would do the work, but we recomend a bigger machine to process the ceremony faster.

In this tutorial I'll describe all the steps required to run them in a new m5a.4xlarge aws instance with ubuntu 20.04.  But this is just for reference. It's better if you run your own hardware.

### Preparation of the machine.

You can use any machine to run the ceremony. The important part of the ceremony is that the toxic value is not leaked and it's deleted after the completion of the ceremony.

This toxic value is in the memory while the ceremony is running. This toxic value is not displayed any where, and it's recomended to restart the machine after the ceremony is completed to be sure this toxic value is not accessible any more.

You can check the [phase1 perpetual powers of tau ceremony](https://github.com/weijiekoh/perpetualpowersoftau) used by Hermez for geting ideas.

You will need node version at least v14. For reference we are using v14.8.0

Quick instructions to install node:

````
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
````

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
71d82bff bd8538c2 3563e778 93fde8e7
dea99f07 613a88a0 c6a286de 4decfb39
c3370068 758209b6 cad7bd75 a6ec95dc
79ed6e54 33088783 bab73475 96f6dafc
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

And the circuit of the `withdraw` circuit should be:

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
