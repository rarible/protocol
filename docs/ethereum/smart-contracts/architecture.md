# Smart Contract Architecture

Rarible exchange smart contracts are built using OpenZeppelin's upgradeable smart contracts library. So the smart contract code can be updated to support new features, fix bugs, etc.

Smart contracts are heavily tested, tests are provided in the test folder.

Functionality is divided into parts \(each responsible for the part of the algorithm\).

Essentially, ExchangeV2 is a smart contract for the decentralized exchange of any assets presented on Ethereum \(or EVM compatible\) blockchain.

