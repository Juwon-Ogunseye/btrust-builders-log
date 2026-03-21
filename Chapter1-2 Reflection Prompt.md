

# Interacting with Bitcoin via CLI vs Libraries

Interacting with Bitcoin via the command line is considered better than using libraries because of **safety**. You will need to trust the developers who created those libraries, and that also means that with one wrong mistake, you could lose all you have. Using Bitcoin via the command line interface means you can actually work and interact with Bitcoin directly and do the right thing.

Bitcoin Core was developed by Bitcoin Core developers and is maintained regularly by them, which means if there is any problem at any time, Bitcoin Core developers will fix it. But when you are using higher-level libraries, there is a high tendency that they won’t fix those bugs, or since they are also dependent on Bitcoin Core, you may inherit those bugs. This is why using Bitcoin via the CLI is considered better.

### Understanding What Happens Under the Hood

Another useful aspect of it is that you understand what is happening under the hood when you are interfacing with Bitcoin Core via the command line. With higher-level libraries, they have taken that aspect away from you so that you can just write code to maybe develop an app.

### CLI vs App Development

Most people using libraries actually want to develop an app—could be a payment app or anything on Bitcoin—and the CLI commands do not give you that opportunity to do that. Bitcoind CLI was built for nodes and not for developers creating apps. They actually created it so you can directly interact with Bitcoin via the RPC.

### Limitations

You also cannot use Bitcoin from mobile; they are too heavy for simple tasks. If you need to build a multisig wallet or a Lightning wallet, it is very complex using bitcoind via command line, and this is what higher-level libraries make simple for developers.

> **Summary:** Using Bitcoin via the command line is mainly for **security**, which is the highest and most beneficial advantage.

---

# Decentralization vs Traditional Payment Systems

Decentralization is resistance against censorship by big corporate organizations such as banks, government, and other forms of institutions that try to control how and what we do with our sovereignty.

Prior to Bitcoin, we had several forms of decentralization that didn’t in any way challenge the payment system. In the 1500s, West African countries such as Nigeria, Ghana, and others used beads as a decentralized means of payment, and when European traders came, they mass-produced beads, which crumbled the financial system, causing hyperinflation in those countries.

Same with North America that used wampum, and the Dutch also mass-produced it and debased their currency.

###  Fiat vs Bitcoin

Till date, the present fiat system is also being mass-produced by the government and those in power. This is where Bitcoin decentralization comes in:

- It cannot be mass-produced
    
- It cannot be copied
    
- It belongs to the users
    

With Bitcoin, there is no need for a central authority, and we are free from mass production and continuous copying.

---

#  Risks of Using `bitcoind` and `lightningd`

###  Financial Risk

One can easily lose funds interacting directly with Bitcoin via bitcoind. One wrong address or fee calculation and your money is gone for good. With other higher-level libraries, some of them add checks for common mistakes like incomplete addresses or high fees, which bitcoind does not add.

###  Storage & Accessibility

Mainnet is about **700GB**, which makes it too large for those with limited space on their PC and also those with poor internet accessibility especially in third world countries. This will also become an issue.

###  Mobile Limitations

Running bitcoind on mobile applications is also not possible because of the size of the node—it is too big for a mobile application and it will crash.

### Developer Limitations

- Not designed for app development
    
- Meant to run a node
    
- Not beginner-friendly
    

You will need to:

- Construct wallets manually
    
- Handle transactions yourself
    
- Understand fees and UTXOs
    

---

#  Benefits of Using CLI

###  Security

The number one benefit is safety over any higher-level libraries. When you interact via the command line, you are sure you are talking directly to a trusted node because you set it up yourself. You don’t need to trust a third party.

### Deep Understanding

You get to understand:

- How fees are calculated
    
- How UTXOs work
    
- Wallet creation and funding
    

You are literally speaking to Bitcoin and getting a deep understanding of what is happening.

---

#  Pseudonymity in Bitcoin

Because all transaction records in Bitcoin are publicly available on the blockchain, if someone can associate a person with their address, they can automatically track the person.

- Address = pseudonym
    
- Identity unknown → privacy maintained
    
- Identity linked → privacy lost
    

This is why Satoshi suggested using a new address for every transaction to make tracking more difficult.

---

#  Censorship Resistance

Because Bitcoin is decentralized and not controlled by a single central authority, it is difficult to block or censor transactions.

### Traditional Systems:

- Can freeze accounts
    
- Can block transactions
    
- Controlled by banks/government
    

### Bitcoin:

- No central authority
    
- No freezing of funds
    
- True peer-to-peer system
    

---

# RPC (Remote Procedure Call) in Bitcoin

RPC helps you interact with Bitcoin Core by allowing communication with another system as if it were your own.

### Simple Analogy

You are in Lagos, your brother is in Abuja. You ask him to calculate 5 × 5, he does it and sends back the answer.

That is RPC.

### How It Works with Bitcoin

- Node can be on:
    
    - Local machine
        
    - Raspberry Pi
        
    - AWS server
        
- You send commands via RPC
    
- It processes and returns results
    

>  RPC allows you to control your Bitcoin node remotely from your local machine.


### How do the five major types of Bitcoin nodes differ?

**Mainnet:**  
This is the main blockchain node with real Bitcoin data. They are not for testing, and they are used for real Bitcoin transactions. They are very large at the moment it is over 500GB of data. It runs a full node using proof-of-work algorithms. If you are running a full node, you need to have a significant amount of space, as it is estimated that over 50GB of data are generated annually (could be more now).

---

**Pruned mainnet:**  
What makes this different is that it discards older Bitcoin data that are no longer needed for validation and keeps only the recent required data, reducing storage to as low as around 550MB or more depending on configuration. A pruned node is good for those who don’t have large storage. One of the major disadvantages I read is that it doesn’t support routing Lightning Network payments, but it can still be used as a wallet.

---

**Testnet:**  
These are nodes used for testing. If you are just getting into Bitcoin, it is always better to run your tests and all other learning processes on testnet, as you won’t be using real funds. It is like a dev environment developers use when testing an app. Unlike mainnet and pruned nodes, everything done here is not real or live transactions.

It also has its downside everything here is chaotic sometimes. Blocks are mined irregularly, sometimes nothing happens. People can spam or abuse the system on testnet, and this is where signet comes in.

---

**Signet:**  
They are a more controlled version of testnet and are more reliable. It is designed to have more predictable block production, usually around every 10 minutes. Unlike testnet where anyone can mine freely, signet has controlled block creation, which makes it more stable for testing. But again, they are not real like mainnet.

---

**Pruned-signet:**  
This is just signet but pruned, meaning it keeps only recent data and reduces storage size similar to pruned mainnet.

---

### What are the benefits of using a VPS (Virtual Private Server) for running a Bitcoin node versus a local machine?

One, it is easier to set up using StackScript, and it can be cheaper especially if you need to run a full node. Also, if you are in a country like Nigeria where power supply is unstable, running your node on a VPS is a better option since it stays online 24/7 without interruption.

### How does running a full node contribute to the security and decentralization of the Bitcoin network?

One, it makes the Bitcoin network stronger. The more full nodes that exist, the more distributed and reliable the network becomes.

Two, you don’t need to trust a third party you can validate your own transactions by yourself.

You also make the network more resistant to attacks because the network is spread across many independent nodes, making it harder to compromise.

---

### How does a pruned Bitcoin node differ from an unpruned node, and when should you use each?

A pruned node discards older blockchain data and keeps only the recent required data, making it much smaller than an unpruned node. For example, mainnet can be over 700GB, while pruned nodes can be configured to use a few GB.

So if a developer in Nigeria using Windows, VS Code, and several applications wants to run a full unpruned node, they will need a bigger machine with more storage.

Also, when you use a pruned node, you won’t be able to access or query older transactions because they have been removed, and you also cannot help new nodes sync by serving them full historical data.

---

### What are the differences between Mainnet, Testnet, and Regtest, and in what scenarios would each be used?

Mainnet runs the full node and contains real transactions and real Bitcoin data.

Testnet has test transactions, unstable blocks, and runs on a public network that anyone can join and use for testing.

Regtest runs on a private environment where you control everything. You can create blocks manually and test quickly, and although it is usually just your environment, you can simulate multiple nodes if needed.

Mainnet is used for real production transactions, like creating wallets and sending actual Bitcoin.

Testnet is used to test applications before deploying to mainnet. It is like a public testing environment.

Regtest is used for local development and fast testing in a controlled setup.

---

### What security priorities should be considered when setting up a Bitcoin node on a VPS?

- Firewall configuration: implement a firewall to control incoming and outgoing traffic
    
- Set IP/port configuration: avoid exposing unnecessary ports like 0.0.0.0
    
- Close all unused ports
    
- Set up DDoS protection to prevent flooding attacks
    
- Enable two-factor authentication to make sure only you have access
    

---

### What are the advantages of using a StackScript to set up a Bitcoin Core VPS?

StackScript makes the setup process easier because it automates most of the installation and configuration steps. You don’t have to manually install everything, which reduces stress and saves time.

It also reduces the chances of making mistakes during setup since everything is already pre-configured, and you can get your node running faster compared to doing everything manually.

---

### Why might a developer choose to run a local instance of the Bitcoin blockchain rather than using a remote node?

One reason is trust you don’t have to depend on a third-party node. Everything is running on your own machine, so you are sure the data is accurate.

Another reason is privacy. When using a remote node, your requests can be monitored, but with a local node, everything stays with you.

Also, for development, running locally gives you more control. You can test faster, especially with regtest, and you are not dependent on network delays or external services.



