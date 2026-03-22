# How to Set Up a Bitcoin Regtest Node from Scratch

> A complete guide for Windows and Linux — following the Bitcoin from the Command Line book

---

## Table of Contents

- What is Regtest
- Windows Setup
- Linux Setup
- Key Differences
- Quick Reference Commands

---

## What is Regtest?

Regtest (Regression Test) is a private local Bitcoin blockchain that runs entirely on your computer. It has no connection to the real Bitcoin network and uses no real money.

**Why use Regtest?**

- Mine blocks instantly — no waiting
- Get free test Bitcoin immediately
- Complete privacy — only you exist on the network
- Reset the entire blockchain anytime
- Perfect for learning Bitcoin development safely

---

## PART 1 — WINDOWS

---

### Step 1 — Download Bitcoin Core

Go to [bitcoincore.org/en/download](https://bitcoincore.org/en/download) and download the Windows version. You will see a file named something like:

```
bitcoin-27.x-win64-setup.exe
```

Download it and open your Downloads folder.

---

### Step 2 — Install Bitcoin Core

Double click the installer file and click through all the default options. Let it install completely.

---

### Step 3 — Close the GUI Immediately

Bitcoin Core will open automatically after installation and start syncing mainnet. **Close it immediately** before it downloads anything.

Click **File → Exit** or click the X and confirm you want to stop.

> ⚠️ **Warning:** If you leave it open it will start downloading the entire Bitcoin blockchain which is over 700GB. Always close it right away.

---

### Step 4 — Find Where Bitcoin Core Installed

Open Command Prompt and navigate to the Bitcoin daemon folder:

```cmd
cd "C:\Program Files\Bitcoin\daemon"
```

Verify Bitcoin Core is installed correctly:

```cmd
bitcoind --version
bitcoin-cli --version
```

You should see something like:

```
Bitcoin Core version v27.x.x
```

---

### Step 5 — Edit the bitcoin.conf File

Press **Windows + S** and search for **Notepad**. Right click Notepad and select **"Run as administrator"** then click Yes.

In Notepad click **File → Open** and navigate to:

```
C:\Users\YOUR_USERNAME\AppData\Local\Bitcoin\
```

> 💡 Replace `YOUR_USERNAME` with your actual Windows username. For example: `C:\Users\HP Z BOOK\AppData\Local\Bitcoin\` is my own file path. 

If you cannot see `bitcoin.conf` change the file type dropdown from **"Text Documents (*.txt)"** to **"All Files (_._)"** and the file will appear.

Open `bitcoin.conf` and scroll to the very bottom. Find this section:

```
# Options for regtest
[regtest]
```

Add these lines directly underneath:

```ini
# Options for regtest
[regtest]
fallbackfee=1.0
maxtxfee=1.1
server=1
```

Save with **Ctrl + S** and close Notepad.

---

### Step 6 — Add Bitcoin to PATH (Optional but Recommended)

So you don't have to navigate to the daemon folder every time:

1. Press **Windows + S** and search **"Environment Variables"**
2. Click **"Edit the system environment variables"**
3. Click **"Environment Variables"** button
4. Under System variables find **Path** and click **Edit**
5. Click **New** and paste:

```
C:\Program Files\Bitcoin\daemon
```

6. Click OK on all windows
7. Close and reopen Command Prompt

---

### Step 7 — Start Regtest Node

> ⚠️ **Important:** The `-daemon` flag is **not supported on Windows**. You need two Command Prompt windows.

Open **Command Prompt Window 1** and run:

```cmd
cd "C:\Program Files\Bitcoin\daemon"
bitcoind -regtest
```

Leave this window open. You will see logs scrolling — this is normal. Do not close it.

---

### Step 8 — Run Commands in Second Window

Open a **new Command Prompt Window 2** and run:

```cmd
cd "C:\Program Files\Bitcoin\daemon"
```

Verify the node is running:

```cmd
bitcoin-cli -regtest getblockchaininfo
```

You should see output like this:

```json
{
  "chain": "regtest",
  "blocks": 0,
  "difficulty": 0.000000...
}
```

---

### Step 9 — Create Wallet and Get Bitcoin

Create a wallet:

```cmd
bitcoin-cli -regtest -named createwallet wallet_name="regtest_wallet" descriptors=true
```

Mine 101 blocks instantly:

```cmd
bitcoin-cli -regtest -generate 101
```

> 💡 We mine 101 blocks because Bitcoin requires 100 confirmations before a coinbase reward can be spent. Block 1's reward becomes spendable after block 101.

Check your balance:

```cmd
bitcoin-cli -regtest getbalance
```

Expected output:

```
50.00000000
```

---

### Step 10 — Stop the Node When Done

Always stop properly. In Window 2 run:

```cmd
bitcoin-cli -regtest stop
```

Then close both windows.

---

---

## PART 2 — LINUX

---

### Step 1 — Download Bitcoin Core

```bash
wget https://bitcoincore.org/bin/bitcoin-core-27.0/bitcoin-27.0-x86_64-linux-gnu.tar.gz
```

---

### Step 2 — Verify the Download

```bash
sha256sum bitcoin-27.0-x86_64-linux-gnu.tar.gz
```

Compare the output against the official checksum on [bitcoincore.org](https://bitcoincore.org/en/download) to confirm the download is genuine.

---

### Step 3 — Extract and Install

```bash
tar -xzf bitcoin-27.0-x86_64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-27.0/bin/*
```

Verify installation:

```bash
bitcoind --version
bitcoin-cli --version
```

---

### Step 4 — Edit bitcoin.conf

Create the Bitcoin config directory if it doesn't exist:

```bash
mkdir -p ~/.bitcoin
```

Open the config file:

```bash
nano ~/.bitcoin/bitcoin.conf
```

Add these lines at the bottom:

```ini
# Options for regtest
[regtest]
fallbackfee=1.0
maxtxfee=1.1
server=1
daemon=1
```

Save with **Ctrl + X**, then **Y**, then **Enter**.

---

### Step 5 — Start Regtest Node

On Linux the `-daemon` flag works so you only need one terminal:

```bash
bitcoind -regtest -daemon
```

The node runs in the background automatically.

---

### Step 6 — Verify the Node is Running

```bash
bitcoin-cli -regtest getblockchaininfo
```

You should see:

```json
{
  "chain": "regtest",
  "blocks": 0,
  "difficulty": 0.000000...
}
```

---

### Step 7 — Create Wallet and Get Bitcoin

Create a wallet:

```bash
bitcoin-cli -regtest -named createwallet wallet_name="regtest_wallet" descriptors=true
```

Mine 101 blocks instantly:

```bash
bitcoin-cli -regtest -generate 101
```

Check your balance:

```bash
bitcoin-cli -regtest getbalance
```

Expected output:

```
50.00000000
```

---

### Step 8 — Stop the Node When Done

```bash
bitcoin-cli -regtest stop
```

---

## Quick Reference Commands

```bash
# Start node
bitcoind -regtest                    # Windows (leave terminal open)
bitcoind -regtest -daemon            # Linux (runs in background)

# Check node info
bitcoin-cli -regtest getblockchaininfo

# Create wallet
bitcoin-cli -regtest -named createwallet wallet_name="regtest_wallet" descriptors=true

# Mine 101 blocks
bitcoin-cli -regtest -generate 101

# Check balance
bitcoin-cli -regtest getbalance

# Get a new address
bitcoin-cli -regtest getnewaddress

# Send Bitcoin
bitcoin-cli -regtest sendtoaddress <address> <amount>

# List transactions
bitcoin-cli -regtest listtransactions

# Stop node
bitcoin-cli -regtest stop

# Reset everything and start fresh (Linux)
rm -rf ~/.bitcoin/regtest

# Reset everything and start fresh (Windows)
# Delete this folder: C:\Users\USERNAME\AppData\Local\Bitcoin\regtest
```

---

## Resources

- [Bitcoin from the Command Line Book](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line)
- [Bitcoin Core Download](https://bitcoincore.org/en/download)
- [Bitcoin Core Documentation](https://bitcoincore.org/en/doc/)
- [Btrust Builders Program](https://btrust.tech/)

---

_Part of the [btrust-builders-log](https://github.com/Juwon-Ogunseye/btrust-builders-log) learning series_