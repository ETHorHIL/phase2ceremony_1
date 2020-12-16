

## Verification of the ceremony

In order to verify the circuit, you will need a machine with tons of memory.

For reference, the one we are using is a machine with 16cores and 512Gb of RAM.

In this tutorial we will give instructions for a x1e.8xlarge aws instance. This instance has 16 cores 32 threads, 976Gb of RAM and it's important to build it with a SSD of 960Gb that we will use as swap space. The instance will use Ubuntu 20.04 and the cost of the instance is 3.336$/h.

So lets start by launching and instece. Be sure to have 1023GB of EBS and local SSD storage.

#### Basic OS preparation

````
sudo apt-get install tmux
````

#### Adding swap and tweeking the OS to accept high amount of memory.

````
sudo mkswap -f /dev/xvdb
sudo swapon /dev/xvdb

sudo sh -c "sed -i '/^\/dev\/xvdb/d' /etc/fstab"
sudo sh -c 'echo "/dev/xvdb      swap        swap    defaults        0 0" >>/etc/fstab'


sudo sh -c 'echo "vm.max_map_count=10000000" >>/etc/sysctl.conf'
sudo sh -c 'echo 10000000 > /proc/sys/vm/max_map_count'
````
#### Compile a patched version of node

First install node with nvm:

````
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
source ~/.bashrc
nvm install v14.8.0
node --version
````

Now compile a patched version of node.  This aptch avoids activating garbage collections in memory presure situations and many threads.  This is very convininet for the optimization program.

````
sudo apt-get update
sudo apt-get install python3 g++ make
git clone git clone https://github.com/nodejs/node.git
cd node
git checkout 8beef5eeb82425b13d447b50beafb04ece7f91b1
patch -p1 <<EOL
index 0097683120..d35fd6e68d 100644
--- a/deps/v8/src/api/api.cc
+++ b/deps/v8/src/api/api.cc
@@ -7986,7 +7986,7 @@ void BigInt::ToWordsArray(int* sign_bit, int* word_count,
 void Isolate::ReportExternalAllocationLimitReached() {
   i::Heap* heap = reinterpret_cast<i::Isolate*>(this)->heap();
   if (heap->gc_state() != i::Heap::NOT_IN_GC) return;
-  heap->ReportExternalMemoryPressure();
+  // heap->ReportExternalMemoryPressure();
 }

 HeapProfiler* Isolate::GetHeapProfiler() {
diff --git a/deps/v8/src/objects/backing-store.cc b/deps/v8/src/objects/backing-store.cc
index bd9f39b7d3..c7d7e58ef3 100644
--- a/deps/v8/src/objects/backing-store.cc
+++ b/deps/v8/src/objects/backing-store.cc
@@ -34,7 +34,7 @@ constexpr bool kUseGuardRegions = false;
 // address space limits needs to be smaller.
 constexpr size_t kAddressSpaceLimit = 0x8000000000L;  // 512 GiB
 #elif V8_TARGET_ARCH_64_BIT
-constexpr size_t kAddressSpaceLimit = 0x10100000000L;  // 1 TiB + 4 GiB
+constexpr size_t kAddressSpaceLimit = 0x40100000000L;  // 4 TiB + 4 GiB
 #else
 constexpr size_t kAddressSpaceLimit = 0xC0000000;  // 3 GiB
 #endif
EOL
./configure
make -j16
````

This will compile a patched version of node.

#### Download and prepare circom

````
cd ~
git clone https://github.com/iden3/circom.git
cd circom
git checkout v0.5.35
npm install
````

#### Prepare the circuits

````
cd ~
git clone https://github.com/hermeznetwork/circuits.git
git checkout phase2ceremony_1
cd circuits
npm install
cd tools
node build-circuit.js create 2000 32 256 64
node build-circuit.js create 376 32 256 64
mkdir withdraw
cd withdraw
cat >withdraw_main.circom <<EOL
include "../../src/withdraw.circom";

component main = Withdraw(32);
EOL
````

#### Compile the circuits

The compilation may take a while. You may want to run this step in `tmux` session.

##### 2000Txs Circuit
````
cd ~/circuits/tools/rollup-2000-32-256-64
node --trace-gc --trace-gc-ignore-scavenger --max-old-space-size=2048000 --initial-old-space-size=2048000 --no-global-gc-scheduling --no-incremental-marking --max-semi-space-size=1024 --initial-heap-size=2048000 ../../../circom/cli.js circuit-2000-32-256-64.circom -f -r -v -n "^RollupTx$|^DecodeTx$|^FeeTx$|^Sha256compression$"
````
##### 376Txs Circtuit
````
cd ~/circuits/tools/rollup-376-32-256-64
node --trace-gc --trace-gc-ignore-scavenger --max-old-space-size=2048000 --initial-old-space-size=2048000 --no-global-gc-scheduling --no-incremental-marking --max-semi-space-size=1024 --initial-heap-size=2048000 ../../../circom/cli.js circuit-376-32-256-64.circom -f -r -v -n "^RollupTx$|^DecodeTx$|^FeeTx$|^Sha256compression$"
````

##### Withdraw Circtuit
````
cd ~/circuits/tools/withdraw
node ../../../circom/cli.js -r -v withdraw_main.circom
````

As you can see the withdraw circuit is run withot -f so circom will aready optimize it.

#### Reaname and check the resulting files:

##### 2000Txs Circuit
````
cd ~/circuits/tools/rollup-2000-32-256-64
mv circuit-2000-32-256-64.r1cs circuit-2000-32-256-64_no.r1cs
b2sum circuit-2000-32-256-64_no.r1cs
````

The result should be:

````
bfa17cf5 0f588868 68303368 4ddff40c
c42f4c8c bb2338f2 0809ae30 bd3d2d85
641a1142 9b2f3b71 132f3b14 4eb147c6
cea1d608 8d75ef21 dd26fc25 ab171517
````

##### 376Txs Circtuit
````
cd ~/circuits/tools/rollup-378-32-256-64
mv circuit-378-32-256-64.r1cs circuit-378-32-256-64_no.r1cs
b2sum circuit-378-32-256-64_no.r1cs
````

The result should be:

````
267999ba 4c556e7b 242df8da 3134b7cc
d6e58bb2 10dd5ae8 ee488c06 e5506312
54c0edcf 518d0ce1 380b92be 33f2b522
d0d35084 280dd702 749a5808 a20802cf
````

##### Withdraw Circtuit

````
cd ~/circuits/tools/withdraw
b2sum withdraw_main.r1cs
````

The result should be:

````
3926b2a3 44e15f3b 2334f124 8ce182c5
44e81b45 5952af44 af4e6d75 321dbb2a
8cbe348e dd07593e 12a8c274 2ad62666
8a8afdb5 45d65843 422400b0 b211e8b0
````

#### Optimize the circuits

#### Verify the zkey file.

#### Verify the attestations.

#### Make a public post.

If you reach this point, it would be great if you can publish a public post or at least a tweet explaining that you verified the circuits.

For any incident you find, please do not hesitate to contact us in the Hermez discord channel or in [ the telegram group](https://t.me/hermez_network)



