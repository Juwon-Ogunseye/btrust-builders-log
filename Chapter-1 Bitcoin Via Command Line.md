

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

### 🚨 Financial Risk

One can easily lose funds interacting directly with Bitcoin via bitcoind. One wrong address or fee calculation and your money is gone for good. With other higher-level libraries, some of them add checks for common mistakes like incomplete addresses or high fees, which bitcoind does not add.

###  Storage & Accessibility

Mainnet is about **700GB**, which makes it too large for those with limited space on their PC and also those with poor internet accessibility. This will also become an issue.

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

