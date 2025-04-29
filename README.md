# 🗳️ Online Voting System
A lab-scale mini-project illustrating how to implement a secure, transparent, and tamper-proof voting mechanism using a single Ethereum smart contract. You will focus entirely on the `Voting.sol` file in Solidity—defining election rules, candidate management, voter authorization, ballot casting, and result retrieval—without writing any front-end or server code.

---
## Overview

Traditional elections rely on centralized authorities and manual counting, which can be slow, opaque, and prone to error or manipulation. By encoding the entire election process in a blockchain smart contract, we remove trust from any single entity, guarantee immutability of recorded votes, and enable anyone to audit results in real time. This lab exercise centers on a single Solidity file—`Voting.sol`—that you will compile, deploy, and interact with using Remix IDE and MetaMask on a public testnet or local simulator.

---

## Key Concepts

- **Immutability**  
  Every vote is stored as a blockchain transaction that cannot be altered or deleted once confirmed.

- **Decentralization**  
  No central server is needed: the Ethereum network enforces contract logic and state transitions.

- **Access Control**  
  Only the contract owner may perform administrative tasks (start/stop elections, register candidates, authorize voters).

- **One-Person-One-Vote**  
  Each authorized address can cast exactly one ballot, enforced by on-chain checks.

- **Transparency & Auditability**  
  A public view function exposes live vote tallies for all candidates without consuming gas.

---

## Contract Structure

Your `Voting.sol` file is organized into five focused modules:

1. **Ownership & Initialization**  
   - Sets the deployer as the owner.  
   - Allows owner to call `startElection(string name)` and `endElection()`.

2. **Candidate Management**  
   - `addCandidate(string name)`: Owner adds a candidate to a dynamic array.  
   - Internally stores each candidate’s name and vote count.

3. **Voter Authorization**  
   - `authorizeVoter(address voter)`: Owner whitelists an address.  
   - Maintains a mapping to track permitted voters.

4. **Ballot Casting**  
   - `vote(uint candidateIndex)`: Authorized addresses call to cast a ballot.  
   - Ensures each address can vote only once using a “hasVoted” mapping.

5. **Result Retrieval**  
   - `getResults()`: Public view returns an array of all candidates’ vote counts.  
   - Gas-free reading supports live dashboards or audit scripts.

---

## How to Use

1. **Download** the `Voting.sol` file into Remix IDE.  
2. **Compile** with Solidity compiler v0.8.x.  
3. **Deploy** to a network (Injected Web3 for Goerli/Sepolia or JavaScript VM).  
4. **Interact** via Remix’s Deployed Contracts panel:
   - Call `startElection("Election Title")`.  
   - Add candidates: `addCandidate("Alice")`, `addCandidate("Bob")`, etc.  
   - Authorize voters: `authorizeVoter(0xYourAddress)`.  
   - Switch accounts in MetaMask to simulate voters, then call `vote(index)`.  
   - Fetch live tallies with `getResults()`.

---

## Functionality Walkthrough

1. **Start Election**  
   - Opens voting window. All `vote` calls before or after will revert.

2. **Register Candidates**  
   - Dynamically adds entries—no redeployment needed for different races.

3. **Authorize Voters**  
   - Only whitelisted addresses may call `vote`. Others will be reverted.

4. **Cast Ballots**  
   - Each call to `vote` increases the selected candidate’s counter by one.  
   - A mapping prevents the same address from voting twice.

5. **End Election**  
   - Optionally close voting to freeze final counts (if implemented).  
   - After closing, `vote` calls revert, but `getResults` remains open.

---

## Remix Deployment Steps

1. **Open Remix IDE** at https://remix.ethereum.org/  
2. **Create** a new file `Voting.sol` and paste in your contract code.  
3. **Compile** using the Solidity compiler plugin (v0.8.x).  
4. **Switch** to the “Deploy & Run Transactions” tab.  
   - **Environment**: Select **Injected Web3** (for testnet) or **JavaScript VM** (local).  
   - **Account**: Choose your MetaMask address or VM account.  
5. **Deploy** by clicking the “Deploy” button and confirming in MetaMask (if using testnet).  
6. **Interact** with the deployed instance via the UI that appears below the deploy button.

---

## Testing & Verification

- **Unit Tests** (optional): Write simple JavaScript tests in Remix’s “Solidity Unit Testing” plugin or in Truffle for basic edge cases:  
  - Unauthorized voting attempts  
  - Double-voting prevention  
  - Candidate indexing out of range  

- **Block Explorer**: On testnet deployment, copy the contract address into Goerli/Sepolia Etherscan to view transactions, events, and contract ABI.

---
> **Note:** This lab only requires the `Voting.sol` contract and the steps to deploy and interact with it in Remix IDE—no front-end or server code is needed.
