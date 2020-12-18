
# How to Contribute Guide

First of all, register yourself in [this form](https://forms.gle/P2Kwuqew94FosvWq5). We will add you to the #trusted-setup-phase2-ceremony channel in the Hermez Discord.

You can also reach us in the [Hermez Telegram group](https://t.me/hermez_network).

## Requirements

A machine with 4 cores and 16Gb would do the work, but we recommend a bigger machine to process the ceremony faster.

In this tutorial I'll describe all the steps required to run them in a new m5a.4xlarge AWS instance with ubuntu 20.04. The actual cost of this instance at the moment of writing is 0.644$/h  But this is just for reference. Actually, it's better if you run your own hardware.

You can use any machine to run the ceremony. The important part of the ceremony is that the toxic value is not leaked and it's deleted after the completion of the ceremony.

This toxic value is in the memory while the ceremony is running. This toxic value is not displayed anywhere and it's not stored anywhere. It's recomended to restart the machine after the ceremony is completed to be sure this toxic value is not accessible any more.

You can check the [Phase1 Perpetual Powers of Tau Ceremony](https://github.com/weijiekoh/perpetualpowersoftau) used by Hermez for geting ideas of what to do to be sure the toxic value is deleted.

## Preparation of the Machine.

You will need node version at least v14. For reference we are using v14.8.0

Quick instructions to install node if you don't have it:

````
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
source ~/.bashrc
nvm install v14.8.0
node --version
````

Install snarkjs:

````bash
npm install -g snarkjs
````

At the begining of the contribution you will receive 3 files:

* `circuit-2000-32-256-64_hez1_xxxx.zkey`
* `circuit-376-32-256-64_hez1_xxxx.zkey`
* `withdraw_hez1_xxxx.zkey`

Where `xxxx` is the contribution of the last participant.

````
wget https://hermez.s3-eu-west-1.amazonaws.com/withdraw_hez1_xxxx.zkey
wget https://hermez.s3-eu-west-1.amazonaws.com/circuit-376-32-256-64_hez1_xxxx.zkey
wget https://hermez.s3-eu-west-1.amazonaws.com/circuit-2000-32-256-64_hez1_xxxx.zkey
````

Take note of the blake2b of the inputs and check with the ceremony coordinator the integrity of the files:
````bash
b2sum circuit-2000-32-256-64_hez1_xxxx.zkey
b2sum circuit-375-32-256-64_hez1_xxxx.zkey
b2sum withdraw_hez1_xxxx.zkey
````

To run the ceremony you need to run:

````bash
snarkjs zkey contribute circuit-2000-32-256-64_hez1_xxxx.zkey circuit-2000-32-256-64_hez1_yyyy.zkey -v -n=yourName
````

Substitute `yourName` for the name you want to appear in the file. Please do not uses spaces or special characters so we don't have problems.  This name is important because this is what will be displayed, together with the contribution hash when all the contributions are listed in the final zkey file verification.

Substitute also `yyyy` by the actual contrubution.  This should be `xxxx` + 1.

Write down the Circuit Hash and The Contribution Hash printed at the end.

The circuit hash for the 2000Txs circuit should be:

````
71d82bff bd8538c2 3563e778 93fde8e7
dea99f07 613a88a0 c6a286de 4decfb39
c3370068 758209b6 cad7bd75 a6ec95dc
79ed6e54 33088783 bab73475 96f6dafc
````

This Hash is computed at the phase two preparation, and depends on the r1cs file and the Powers of Tau result ceremony.

Do the same for the other two circuits:

````bash
snarkjs zkey contribute circuit-376-32-256-64_hez1_xxxx.zkey circuit-376-32-256-64_hez1_yyyy.zkey -v -n=yourName
snarkjs zkey contribute withdraw_hez1_xxxx.zkey withdraw_hez1_yyyy.zkey -v -n=yourName
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

Now you can compute the checksum of your contribution results.

````bash
b2sum circuit-2000-32-256-64_hez1_yyyy.zkey
b2sum circuit-375-32-256-64_hez1_yyyy.zkey
b2sum withdraw_hez1_yyyy.zkey
````

With this, you will have all the information to fill the attestation template.

Create a copy of the [template_attestation.md](template_attestation.md) with name `yyyy_yourName_attestation.txt`

Fill all the fields of the template.

Sign the template with a PGP key or Keybase.

And generate a signed attestation with name:
`yyyy_yourName_attestation_signed.txt`


Send the 3 responses plus the signed attestation to the coordinator.

You will be asked to do so by first creating a ssh-key if you don't have it.

````bash
ssh-keygen -t rsa -q -f "$HOME/.ssh/id_rsa" -N ""
````

Send the public key to the ceremony coordinator.
You can see your public key by typing:

````bash
cat ~/.ssh/id_rsa.pub
````

Once the ceremony coordinator authorizes your key, you can upload the generated files and the signed attestation by doing:

````bash
sftp contributor_yyyy@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put circuit-2000-32-256-64_hez1_yyyy.zkey'
sftp contributor_yyyy@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put circuit-376-32-256-64_hez1_yyyy.zkey'
sftp contributor_yyyy@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put withdraw_hez1_yyyy.zkey'
sftp contributor_yyyy@s-628cadcefdfd40e39.server.transfer.us-east-1.amazonaws.com <<< $'put yyyy_YourName_attestation_signed.txt'
````

Send also your public PGP Key or a link to yout PGP keybase to the coordinator.

Thank you very much for contributing!
