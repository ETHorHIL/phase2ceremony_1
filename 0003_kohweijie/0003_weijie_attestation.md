# Hermez First Phase 2 ceremony attestation

**Contribution Number:** 0003

**Name:** Koh Wei Jie

**Date:** Dec 20th, 2020

**Location:** The cloud

**Device:** Google Cloud VM n2d-standard-4 (4 vCPUs, 16 GB memory),
Confidential VM service enabled

I used a Google Cloud account enrolled in [Google's Advanced Protection
Program](https://landing.google.com/advancedprotection/). The Confidential
Computing option purports to provide encryption to data in the cloud while it
is being processed. I can't speak to whether this service is truly secure, but
generally, the more diverse the hardware/VMs used, the more secure the
ceremony. As such, even if Confidential Computing is only as secure than a
regular Google Cloud VM, an adversary will have the already difficult task of
compromising Google Cloud in addition to compromising every other participant's
device.

**Entropy sources:** Keyboard mashing and hex values from [the Australian
National University's Quantum Random Number
Generator](https://qrng.anu.edu.au/random-hex/).

`lscpu` output:

```
Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              4
On-line CPU(s) list: 0-3
Thread(s) per core:  2
Core(s) per socket:  2
Socket(s):           1
NUMA node(s):        1
Vendor ID:           AuthenticAMD
CPU family:          23
Model:               49
Model name:          AMD EPYC 7B12
Stepping:            0
CPU MHz:             2249.998
BogoMIPS:            4499.99
Hypervisor vendor:   KVM
Virtualization type: full
L1d cache:           32K
L1i cache:           32K
L2 cache:            512K
L3 cache:            16384K
NUMA node0 CPU(s):   0-3
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl no
nstop_tsc cpuid extd_apicid tsc_known_freq pni pclmulqdq ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm cmp_legacy cr8_legacy abm sse4a misalignsse 3dnowpre
fetch osvw topoext ssbd ibrs ibpb stibp vmmcall fsgsbase tsc_adjust bmi1 avx2 smep bmi2 rdseed adx smap clflushopt clwb sha_ni xsaveopt xsavec xgetbv1 clzero xsaveerptr arat npt nrip_save umip rdp
id
```

I downloaded the following file and checked that their Blake2 hashes match
those attested by the previous participant.

```
circuit-2000-32-256-64_hez1_0002.zkey
f7a0e5b48d8b1ea6a1fa8289bc13d77348a1f469886cd6509301eeb1711cd0c863dc88ded41c9a289619a486c2a53de1f459f6e9d8aa522de8ea5959babd52c8

circuit-376-32-256-64_hez1_0002.zkey
80cb6b10ef133681cb7d9abac5ebc070cade268b51796356469ad8aa19dab908afb94e10fd2e651d3add8515d7bb2bb2013437fa534be0f8636acdbc10f68e85

withdraw_hez1_0002.zkey
dbbcc22dee8330207ba75063f244da8c1f5aca40c273445fd366763ccad23d7a7dd12ba6f686f6d2b0bb38ae79f7f3d9ed5073041c298b7ed4b5c5fa61054d0e
```

## My contributions

`snarkjs zkey contribute circuit-376-32-256-64_hez1_0002.zkey circuit-376-32-256-64_hez1_0003.zkey -v -n=kohweijie`

```
[INFO]  snarkJS: Circuit Hash: 
                d357a1ec f80bbc0e ba06ae34 4a40c688
                79026153 c5a1c550 28b6ac02 3789d26c
                b3c59f9b eb74cd2e 13f7ce35 7f2b18fd
                08dc9f7f 1abf46f6 98f6a5c4 a8b2ce98
[INFO]  snarkJS: Contribution Hash: 
                d91a93c1 2d86371d 6d7e249e df5bfadf
                c1730bce a091ef6c e50448ce e64b6408
                458ea025 0fbc0a91 90b1e0d8 30e930b2
                f462c17f 2b04bf15 620e0836 61efd302
```

Time taken: 2.6 hours


`time snarkjs zkey contribute circuit-2000-32-256-64_hez1_0002.zkey circuit-2000-32-256-64_hez1_0003.zkey -v -n=kohweijie`

```
[INFO]  snarkJS: Circuit Hash:
                71d82bff bd8538c2 3563e778 93fde8e7
                dea99f07 613a88a0 c6a286de 4decfb39
                c3370068 758209b6 cad7bd75 a6ec95dc
                79ed6e54 33088783 bab73475 96f6dafc
[INFO]  snarkJS: Contribution Hash:
                e8232b4e aa4fb6ca 25cdcef7 02cb98e9
                a8f06cf5 5cdcc296 eec200dc cf4507b3
                ce5a1483 9a4b97ad 562a6d93 9ed92fa3
                0d707e18 fdd3c598 e1fa2d3f 946c6747
```

Time taken: 10 hours

`snarkjs zkey contribute withdraw_hez1_0002.zkey withdraw_hez1_0003.zkey -v -n=kohweijie`

```
[INFO]  snarkJS: Circuit Hash: 
                ec15023b 4b03e104 a8b8f620 e48b6f8a
                f6231eeb d3a3e47c c7745379 34b16062
                301a0ad3 91d56c7e cf98b8d3 28f231f5
                42f67e89 893e2b21 277e7019 55020b8c
[INFO]  snarkJS: Contribution Hash: 
                39b8bc7f 213fdff6 d253da9f 3ea547bf
                32185495 92d73d60 3bf44c61 b2cdbcfc
                4f68b634 39424289 fcdbd46e d4372eb7
                cec1dc2f d889938f caca994b 56abe2dc
```

Time taken: less than 5 minutes
