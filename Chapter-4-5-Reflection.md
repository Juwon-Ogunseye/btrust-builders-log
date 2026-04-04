**What are the different methods for sending Bitcoin transactions using `bitcoin-cli`?**  
using direct method and simple commands to send to an address in this method you first set your min transaction fee from your bitcoin.conf at least 10,000 sat for fee then you can get the receiver address and just use your command via the cli

`bitcoin-cli -regtest sendtoaddress $receiver_add 10`

using raw transaction in this one you have to know the utxo you have on ground by running

`bitcoin-cli -regtest listunspent`

and then you see all the utxo available you can go ahead and create variables for your address you want to send funds to, for vout, for txid and then you write the raw transaction they are in json format you can use jq to make accessing keys and values easier this is a basic format used in writing raw transactions

`bitcoin-cli createrawtransaction '[{"txid":"'$your_txid'","vout":'$your_vout'}]' '{"'$your_recipient'":bitcoin_amount}'`

the last one is by using a change address this one makes it in a way that you send your bitcoin and then calculate the fee then use change address to send the rest into it change address is like using getnewaddress this is an example

`bitcoin-cli -named createrawtransaction inputs='[{"txid":"'$utxo_txid_1'","vout":'$utxo_vout_1'},{"txid":"'$utxo_txid_2'","vout":'$utxo_vout_2'}]' outputs='{"'$recipient'":0.009,"'$changeaddress'":0.0009}'`

it is very similar to using raw transaction just that with raw transaction you might send the entire utxo if you are not careful but with this you can send what you want and return the rest back to yourself using change address

---

**What is the difference between Legacy and SegWit transactions?**  
legacy is the first type of wallet address created and they are most used and most compatible and they start with 1 so if you see an address that starts with 1 just know it is legacy but they are more expensive to use

segwit address are cheaper because they separate the signature from the transaction they are two types nested and native segwit

nested segwit are lower fees support multisignature start with 3 and are more compatible but still more expensive than bech32

native segwit are case insensitive lowest transaction fees but not all wallets support it

imagine if you receive several cheques from your dad everyday for one year and you need to cash them at the bank knowing fully well that the most important and delicate part is the signature which takes time for the bank staff to verify for every cheque

now imagine when you get there they remove all the signatures from the cheques and focus on just the data amount sender and receiver while another staff handles all the signatures separately that is exactly how segregated witness works

they move the signature away from the main transaction since about 60 percent of the size of a transaction is signature by separating it we reduce the size of each transaction and that is why segwit transactions are cheaper and more efficient

---

**How do transaction fees work and how are they determined**  
transaction fees are based on the size of the transaction in bytes not really the amount you are sending so the bigger your transaction size the higher the fee this depends on how many inputs and outputs you have if you are combining many utxo your transaction becomes bigger

fees are also determined by network demand when the network is busy you have to pay higher fees for miners to include your transaction faster if not your transaction might stay pending

you can also set fees manually or let bitcoin core estimate it automatically

---

**What are the risks and dangers associated with raw transactions**  
miscalculation is a big one and if you are using raw transactions you have to be very careful because one mistake and you lose your funds

if you forget to include a change address you might send everything to the recipient or lose it as fees

also if you miscalculate the fee your transaction can get stuck or you overpay

raw transactions give you full control but that also means full responsibility no safety checks like normal wallet

---

**How can you use `bitcoin-cli` to send Bitcoin in the simplest way**  
by just starting up your node getting the receiver address and using a simple command like

`bitcoin-cli sendtoaddress $recipient 0.001`

---

**What are the benefits of using named arguments when creating raw transactions**  
normal command line arguments rely on position you pass values in a specific order and bitcoin core assumes what each value means based on where it appears

for example without named arguments

`bitcoin-cli -regtest createwallet "mywallet" false false "" false true`

you really do not know what each value stands for

with named arguments

`bitcoin-cli -regtest -named createwallet wallet_name="mywallet" descriptors=true`

named arguments let you explicitly say which value belongs to which parameter so it reduces errors and makes your command easier to read

---

**How can automation be used to send raw Bitcoin transactions**  
automation can be done using bash scripts to handle everything from getting utxo creating raw transaction signing and broadcasting

you can store values in variables and reuse them instead of typing everything manually which reduces mistakes and saves time

you can also build systems that automatically send bitcoin when certain conditions are met

---

**How does `jq` help when working with Bitcoin transactions**  
jq helps you parse and extract data from json output since most bitcoin cli responses are in json

instead of manually going through everything you can use jq to pick specific values like txid amount or address

this makes scripting easier and cleaner especially when working with raw transactions

---

**What role does `curl` play in sending Bitcoin transactions via command line tools**  
curl is used to interact with the bitcoin core rpc interface directly you can send http requests to your node to create sign and broadcast transactions

it is useful when you are not using bitcoin-cli and want to build custom tools or integrate bitcoin into applications

you send json rpc requests using curl and get responses back from the node

CHAPTER 5 
**What is the mempool and how does it affect Bitcoin transactions**  
mempool is just like a waiting area where unconfirmed transactions stay before miners pick them

when you send bitcoin it does not go straight into a block it first goes there and waits

so if your fee is low it can just sit there for long especially if network is busy and sometimes it might not even get picked at all

---

**How do Replace By Fee RBF and Child Pays For Parent CPFP mechanisms differ in resolving unconfirmed transactions**  
rbf is basically you replacing your transaction with another one with higher fee so miners will pick the new one instead

cpfp is not replacing anything you just create another transaction that depends on the first one and put higher fee on it

so miners will just take both because of the higher total fee

---

**How do you determine if a bitcoin transaction is stuck**  
if it is taking too long and still zero confirmation then it is likely stuck

you can check using explorer or cli and see if it has not moved

most times it is just low fee compared to what others are paying

---

**How does RBF help in modifying an unconfirmed transaction**  
rbf lets you resend that same transaction but with higher fee

so the old one kind of gets replaced and miners go for the new one

but it only works if you enabled it from the start

---

**How does CPFP allow a child transaction to push a parent transaction through**  
cpfp works by creating another transaction linked to the first one

then you attach higher fee to the second one so miners include both together

so even if the first one had low fee it still goes through

---

**When should you use RBF versus CPFP**  
use rbf if you are the sender and you still control the transaction

use cpfp if you cannot change the first one or if you are the receiver trying to speed it up

---

**What are the risks of using RBF and CPFP**  
rbf can be risky because transaction can be replaced so double spending is possible

and some platforms do not really trust it

cpfp you might just end up paying more fee than expected

and mistakes in general with transactions can cost you funds

---

**How do miners prioritize transactions in the mempool**  
miners care more about fee rate which is sat per byte not just total fee

so higher fee rate gets picked faster

and sometimes they include linked transactions together because of combined fees

---

**Why does the author argue that BIP32 wallets are a superior wallet**  
bip32 wallets let you generate many addresses from one seed

so you do not need to keep backing up multiple keys

it also improves privacy since you can keep using new addresses

overall it just makes things easier and more organized compared to older wallets