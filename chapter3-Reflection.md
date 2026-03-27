
### What are the basic steps to create a Bitcoin address to receive funds?

first you create a wallet, for me i am using regtest so i will be creating the wallet with `-regtest`.

first what is a bitcoin wallet — this is a digital account where your bitcoin is stored. it is like your traditional bank account where you are provided an account number to receive money into and you are also asked to create a security pin, just that in bitcoin your wallet comes with both private and public key which is like your Gtbank account coming with both account number and a password that is only known to you.

first step in creating a bitcoin address is to first create a bitcoin wallet and you can do that via the command line using

```
bitcoin-cli -named createwallet wallet_name="BlackHart_wallet"
```

you can also specify the type of wallet you would like to create, is it legacy, nested segwit, native segwit and each of this segregated witness account have their own benefits.

second then you can now create an address which is like an account number where you give to people to send money into using this line of code

```
bitcoin-cli -regtest getnewaddress -addresstype legacy
```

if you noticed i specify legacy you can select bech32 or p2sh type of address anyone is okay.

---

### What is a descriptor, and how does it relate to address generation?

descriptor is a function that takes an argument in bitcoin. so if i am not using a descriptor and i need to create a wallet address the flow is

walletCreation -> address -> select the type of address

with a descriptor you basically use your single key to help you create more than one address type. one key will generate legacy, nested and native wallet address.

so for example you have this as your public key

k = 03efdee34c

you can derive a legacy here

pkh(k)

same key you can also do wpkh(k) and it will still derive another address for you and so on. in this way you don’t have to be creating new wallet or different type of address so you can use one key for multiple address types.

---

### What are the key files and directories in a Bitcoin node’s file layout?

so by running `tree ~/.bitcoin/regtest` you should see all the files and node layout for your bitcoin.

**blocks:** this contains all the blockchain history. all the transactions received and sent are all stored here and they contain sub folders too

- blk0000.dat
    
- index (a whole lot of files are embedded in this)
    

**chainstate:** this contains the current state of the blockchain. who currently owns bitcoin this is where utxo is. so it is the most important file and also contains subfiles

- current
    
- lock
    
- manifest
    

**mempool.dat**  
**peers.dat**  
**settings.json**

**wallets:** this contains everything about your wallet public, private, descriptor, and all

- database
    
- log.00000001
    
- db.log
    
- wallet.dat
    

### How can you use informational commands in `bitcoin-cli` to understand your node's status?

so one thing i noticed is bitcoin-cli is not just for sending and receiving you can actually use it to check what is going on inside your node.

for example you can run commands like

```
bitcoin-cli -regtest getblockchaininfo
```

this will show you if your node is synced, the number of blocks, and the chain you are on.

you can also check

```
bitcoin-cli getnetworkinfo
```

to see how your node is connected to other peers.

so instead of just assuming everything is working fine you are actually confirming it. it is more like checking your bank app balance before sending money just to be sure everything is correct.

---

### Why is it important to verify your Bitcoin setup before engaging in transactions?

this part is actually very important because bitcoin is not forgiving at all.

if your setup is wrong maybe you are on the wrong network or your wallet is not properly loaded or even your node is not synced and you go ahead to send funds you can lose that money permanently.

so verifying your setup is like double checking everything before taking action.

things like

- confirming you are on regtest or mainnet
    
- making sure your wallet is loaded
    
- checking your balance
    
- making sure your node is synced
    

all this helps you avoid mistakes.

because once you send bitcoin there is no reverse button and no customer care to call.

---

### What are the benefits of using command-line variables when working with Bitcoin Core?

so instead of writing the full command every single time you can define variables and reuse them.

for example you can store

```
cli="bitcoin-cli -regtest"
```

so instead of writing the long command again and again you just do

```
$cli getblockchaininfo
```

this makes your work faster and reduces mistakes because sometimes you might forget to add `-regtest` and end up running command on the wrong network.

it also makes your script cleaner especially when you are doing multiple commands.

so it is more like creating a shortcut for yourself so you don’t keep repeating the same thing.
