# Hemi-Network-CLI-PoP-Miner-Full-Guide

# CLI PoP Miner

### 📜 **TL;DR (Too Long; Didn't Read)**

* This guide provides straightforward steps to download, set up, and run your PoP Miner, either by downloading **pre-built binaries** or by **building from source**.
* Ensure you have your development environment ready and follow the steps below to join the mining network.
* To start mining, claim tBTC via the Hemi [Discord faucet](https://discord.gg/hemixyz) or send at least `0.002 tBTC` to your provided Bitcoin testnet address and run the miner with your private key.

***

## 🏁 Prerequisites

* **tBTC** - Join the Hemi [Discord](https://discord.gg/hemixyz) and visit our `#faucet` channel to acquire tBTC.

***

## 📚 Tutorial

### 1️⃣. Binaries

[Download a pre-built binary](https://github.com/hemilabs/heminetwork/releases) or [build from source using the README](https://github.com/hemilabs/heminetwork?tab=readme-ov-file#-building-from-source). Choose the release you want to use (_if unsure, choose the latest_), and click on `Assets` dropdown:

<figure><img src="../../.gitbook/assets/pop-miner-binaries-v0.2.8 (1).png" alt=""><figcaption><p>Note: the version numbers may be different.</p></figcaption></figure>

The package you will need to download depends on your OS and architecture:

* **Windows (Intel/AMD CPU):** heminetwork\_v0.2.8\_windows\_amd64.zip
* **Mac (Intel CPU):** heminetwork\_v0.2.8\_darwin\_amd64.tar.gz
* **Mac (Apple Silicon "M" CPU):** heminetwork\_v0.2.8\_darwin\_arm64.tar.gz
* **Linux (Intel/AMD CPU):** heminetwork\_v0.2.8\_linux\_amd64.tar.gz
* **Linux (ARM CPU):** heminetwork\_v0.2.8\_linux\_arm64.tar.gz

***

### 2️⃣. Extract the files

After downloading the necessary files, you must extract them from their compressed format before you can use or access the software. On most operating systems, you can right-click on the downloaded archive and choose "Extract" or similar.&#x20;

**Linux/macOS tip**:&#x20;

You can also use the command `tar xvf heminetwork_v0.2.8_linux_amd64.tar.gz`\
\
Run the  `uname -a` command in the Terminal to view all system information, ensuring compatibility with the correct asset on GitHub. \
\
Depending on the output:\
"**x86\_64**" => Choose the "**amd64**" package corresponding to your OS\
"**arm64**" => Choose the "**arm64**" package corresponding to your OS

***

### 3️⃣. Open your CLI and navigate to the extracted folder

Launch your CLI:

**For Windows:**

* Press `⊞ Win` + `R` together to open the "Run Program Or File" Window
* Type "cmd" and press `Enter`


**For macOS:**

* Press `⌘` + `Space` together to open Spotlight Search
* Type "terminal" and press Enter

\
**For Linux:**

* Depends on OS. On Ubuntu (Gnome): `Ctrl` + `Alt` + `T`
* For most other distros, you can press `Super` (Windows Key) and search for Terminal.&#x20;


Navigate to the folder you extracted by typing `cd` (**don't press `Enter` ye**t) and then drag the path of the extracted folder into your CLI, or type the path in manually and then press `Enter`.

* For example on Windows if you downloaded the package to your Downloads folder and extracted it through the GUI, you might run a command like:\
  \
  `cd '/home/user/Downloads/heminetwork_v0.4.3_windows_amd64'`

***

### 4️⃣. Confirm folder contents

List the files:

**For Windows:**

* `dir`  (and press `Enter`)

**For macOS:**

* `ls`  (and press `Enter`)

Your output should be:

*   **Linux & macOS**

    ```none
    bfgd    bssd    extool    hemictl    keygen    popmd    tbcd
    ```
*   **For Windows**

    ```
    bfgd.exe    bssd.exe    extool.exe     hemictl.exe     keygen.exe     popmd.exe     tbcd.exe
    ```

***

### 5️⃣. Verify configuration success

To ensure you downloaded the correct binaries and are able to run them, execute the command below:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Linux &#x26; macOS</strong></td><td><p><mark style="color:purple;">⚠️ On Mac you will need to first remove the quarantine by running the following command in your Terminal:</mark></p><p><mark style="color:purple;"><code>xattr -d com.apple.quarantine ./popmd</code></mark><br><br></code></p></td><td><strong>Run</strong></p><p><code>./popmd --help</td></tr><tr><td><strong>Windows</strong></td><td><mark style="color:purple;">⚠️ <strong>Important Note for Windows Users</strong>: To successfully execute this command, you must use the Command Prompt (CMD), not PowerShell (which is the default terminal in environments like Visual Studio Code).</mark></td><td><p></p><p><strong>Run</strong></p><p><code>popmd.exe --help</code></p></td></tr></tbody></table>

This will display the help menu for `popmd`, indicating that it's installed and operational.

```
Hemi Proof of Proof miner: v0.1.0-pre+f09d4e5ff
Usage:
	help (this help)
Environment:
	POPM_BFG_URL           : url for BFG (Bitcoin Finality Governor) (default: http://localhost:8383/v1/ws/public)
	POPM_BTC_CHAIN_NAME    : the name of the bitcoin chain to connect to (ex. "mainnet", "testnet3") (default: testnet3)
	POPM_BTC_PRIVKEY       : bitcoin private key (required) 
	POPM_LOG_LEVEL         : loglevel for various packages; INFO, DEBUG and TRACE (default: popmd=INFO;popm=INFO)
	POPM_PPROF_ADDRESS     : address and port popm pprof listens on (open <address>/debug/pprof to see available profiles) 
	POPM_PROMETHEUS_ADDRESS: address and port popm prometheus listens on 
	POPM_REMINE_THRESHOLD  : the number of L2 Keystones behind the latest seen that we are willing to remine, this is handy for re-orgs (default: 0)
	POPM_STATIC_FEE        : specify the number of sats/vB the PoP Miner will pay for fees (default: 1)
```

***

### 6️⃣🅰️. Generate public key

If you prefer to PoP mine using a preexisting private key, you may skip this step. **You may import a private key from either an EVM or BTC address.**

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Linux &#x26; macOS</strong></td><td><p><mark style="color:purple;">⚠️ On Mac you will need to remove the quarantine by running:</mark></p><p><mark style="color:purple;"><code>xattr -d com.apple.quarantine ./keygen</code></mark></p></td><td><p><strong>Run the following command:</strong></p><pre data-overflow="wrap"><code>./keygen -secp256k1 -json -net="testnet" > ~/popm-address.json
</code></pre></td></tr><tr><td><strong>Windows</strong></td><td><p><mark style="color:purple;">⚠️ <strong>Important Note for Windows Users</strong>: To successfully execute this command, you must use the Command Prompt, not PowerShell (which is the default terminal in environments like Visual Studio Code). Follow these steps to open Command Prompt:</mark></p><ol><li><mark style="color:purple;">Click on the <strong>Start Menu</strong> button or press the <strong>Windows</strong> key on your keyboard.</mark></li><li><mark style="color:purple;">Type <strong><code>cmd</code></strong></mark> <mark style="color:purple;">into the search bar and open it.</mark></li><li>Type the following command and press Enter:</li></ol></td><td><pre><code><strong>keygen.exe -secp256k1 -json -net="testnet" > "PATH\popm-address.json" 
</strong></code></pre><p><strong>Note:</strong> After running the command, you might not see any immediate feedback in the Command Prompt. This is expected behavior.</p><ol start="4"><li>Open the generated key file</li></ol><p>After generating the key file, you'll want to check its contents. To do this, use the following command in Command Prompt:</p><pre class="language-cmd" data-overflow="wrap"><code class="lang-cmd">%HOMEDRIVE%%HOMEPATH%\popm-address.json
</code></pre><p>This command opens the <code>popm-address.json</code> file in Notepad, allowing you to view or edit the generated key.</p></td></tr></tbody></table>

### 6️⃣🅱️. Open the JSON

If you chose to generate a new private key in Step 6a, open your JSON to view your file contents.&#x20;

**On Windows:** See the above instructions for how to open the file in Notepad.

**On Linux/macOS:** Run the following command to print the contents of your key file to the Terminal:\
\
`cat ~/popm-address.json`

You should see a result like:

```
{
  "ethereum_address": "0x12345FabcD298299b8250e16eEb7D6a7B81DfEdC",
  "network": "testnet",
  "private_key": "123456789abcdef123456789abcdef123456789abcdef123456789abcdef1234",
  "public_key": "04123456789abcdef123456789abcdef123456789abcdef123456789abcdef12345678abcdef123456789abcdef123456789abcdef123456789abcdef1234",
  "pubkey_hash": "m12345678P2xVWwVCWxq7tHJLGcJz2h6XYZ"
}
```

***

### 7️⃣. Fund your address

Find your wallet address:&#x20;

* **New Address:** If you generated a new public key in Step 6a, check the JSON file from Step 6b for your `pubkey_hash`.&#x20;
* **Existing BTC Address:** If you are importing a private key from an existing BTC address, change your wallet type to P2PKH (Legacy) and locate the public key.
* **Existing EVM Address:** If you are importing a private key from an existing EVM address, [import your private key into UniSat](btc-wallet-setup/) and select P2PKH (Legacy) as your wallet type.

Fund your wallet:&#x20;

* Claim tBTC in the [Hemi Discord faucet](https://discord.gg/hemixyz) to send at least`0.002 tBTC` to your `pubkey_hash` address.
* You can also get tBTC from faucets [like this one](https://coinfaucet.eu/en/btc-testnet/). However, these faucets often don't provide enough tBTC to do much PoP mining.&#x20;

***

### 8️⃣. Run the Miner

In your console, execute the following commands while:

1. replacing `private_key` with either the value from your JSON file in Step 5 **OR** your preexisting EVM/BTC private key,
2. replacing `fee_per_vB_integer` with the fee in sat/vB you want to pay.&#x20;

Read the [**"Bitcoin fee/vB"**](setup-part-1.md#bitcoin-fee-vb) section below if you need help determining what value to set here.&#x20;

**Linux & macOS**

```
export POPM_BTC_PRIVKEY=private_key
export POPM_STATIC_FEE=fee_per_vB_integer
export POPM_BFG_URL=wss://testnet.rpc.hemi.network/v1/ws/public
./popmd
```

**Windows**

```
set POPM_BTC_PRIVKEY=private_key
set POPM_STATIC_FEE=fee_per_vB_integer
set POPM_BFG_URL=wss://testnet.rpc.hemi.network/v1/ws/public 
popmd.exe
```

***

### 9️⃣. Expected Console Output

<pre class="language-none"><code class="lang-none">2024-09-19 23:03:46 INFO popmd popmd.go:111 Hemi Proof-of-Proof Miner v0.4.3+0c53c8654 (Hemi Labs, popmd, go1.23.1 darwin/arm64)
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_BFG_URL           : wss://testnet.rpc.hemi.network/v1/ws/public
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_BTC_CHAIN_NAME    : testnet3
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_BTC_PRIVKEY       : ********
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_LOG_LEVEL         : popmd=INFO;popm=INFO
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_PPROF_ADDRESS     : 
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_PROMETHEUS_ADDRESS: 
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_REMINE_THRESHOLD  : 0
2024-09-19 23:03:46 INFO popmd popmd.go:115 POPM_STATIC_FEE        : 150
2024-09-19 23:03:46 INFO popm popm.go:954 Starting PoP miner with BTC address n3vTV2wz5wEqiX1rx4aE2LJ19himfXKxQY (public key 031865e70e33c70a741a00a9b262f4a83947c69c725dc9c14f98117e789ae8673f)
<strong>2024-09-19 23:03:46 INFO popm popm.go:450 Checking for new keystone headers...
</strong>2024-09-19 23:03:46 INFO popm popm.go:389 checking keystone received with height 88750 against last keystone 88800
2024-09-19 23:03:46 INFO popm popm.go:389 checking keystone received with height 88775 against last keystone 88800
2024-09-19 23:03:46 INFO popm popm.go:389 checking keystone received with height 88800 against last keystone 88800
</code></pre>

***

### 🔟. 🎉 Congrats! You are now a Hemi PoP Miner!

Let us know how this process was for you via [Discord](https://discord.gg/hemixyz). We are constantly looking for ways to improve our documentation.

***

#### **Bitcoin fee/vB**

The Bitcoin transaction (normally represented in satsoshis per virtual byte or sats/vB) is a fee paid to the Bitcoin miners to include a transaction in a Bitcoin block. It varies with network congestion, typically rising during periods of high transaction volume and decreasing when there is less activity.&#x20;

* The PoP Miner consumes tBTC to pay the Bitcoin miners to include PoP transactions in Bitcoin blocks.
* In order to ensure PoP transactions from your PoP miner are included in Bitcoin blocks, ensure the configured fee is set to an appropriate value. The PoP miner can be configured to use a certain fee in sats/vB by changing the `POPM_STATIC_FEE` environment variable when running the PoP miner. In a future version, the PoP miner will automatically calculate the current network fee to guarantee PoP transactions are included in Bitcoin blocks.
* The lower you set the fee, the less tBTC you will pay per PoP transaction. But if your fees are too low, Bitcoin miners may not include your transaction quickly enough for you to successfully PoP mine.

**Beginner and intermediate users:**&#x20;

* We recommend setting the `POPM_STATIC_FEE` environment variable to `50` (50 sats/vB) to ensure PoP transactions are included in Bitcoin blocks.

**Advanced users:**&#x20;

1. Check Current Fee Levels: Visit [mempool.space](https://mempool.space/testnet) to see the current fee levels. Look at the "sat/vB" numbers for the different transaction fee priorities. It is recommended to set the value to the "High Priority" value or slightly higher.
2. Set the Static Fee: Re-run the command to set the `POPM_STATIC_FEE` environment variable from above (`export` on Linux/macOS, `set` on Windows) each time you want to change the fee, and restart the PoP Miner afterwards.

🔶For Next Day Run This Command

###1️⃣ Open your CLI and navigate to the extracted folder 

Launch your CLI:

**For Windows:**

* Press `⊞ Win` + `R` together to open the "Run Program Or File" Window
* Type "cmd" and press `Enter`

Navigate to the folder you extracted by typing `cd` (**don't press `Enter` ye**t) and then drag the path of the extracted folder into your CLI, or type the path in manually and then press `Enter`.

* For example on Windows if you downloaded the package to your Downloads folder and extracted it through the GUI, you might run a command like:\
  \
  `cd '/home/user/Downloads/heminetwork_v0.4.3_windows_amd64'`

###2️⃣ Confirm folder contents

**For Windows:**

* `dir`  (and press `Enter`)

###3️⃣ Run the Miner

In your console, execute the following commands while:

1. replacing `private_key` with either the value from your JSON file in Step 5 **OR** your preexisting EVM/BTC private key,
2. replacing `fee_per_vB_integer` with the fee in sat/vB you want to pay.&#x20;

**Windows**

```
set POPM_BTC_PRIVKEY=private_key
set POPM_STATIC_FEE=fee_per_vB_integer
set POPM_BFG_URL=wss://testnet.rpc.hemi.network/v1/ws/public 
popmd.exe
```
