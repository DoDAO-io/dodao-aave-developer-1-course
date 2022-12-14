## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Starter-DApp-Template
 
 
---

##### What programming language is used to write the smart contract in this template?  

- [x]  Solidity
- [ ]  Javascript
- [ ]  C++
- [ ]  Python
  
Hint: NoHint
         
Explanation: Solidity is a programming language for writing smart contracts that run on the Ethereum platform.

Sub Topics: No Sub-Topics
 

---

##### What browser extension is used in this guide to interact with the Ethereum blockchain?  

- [ ]  Solidity
- [x]  MetaMask
- [ ]  Ethers.js
- [ ]  React
  
Hint: Others are not extensions
         
Explanation: MetaMask is a browser extension that allows users to interact with the Ethereum blockchain.

Sub Topics: No Sub-Topics
 

---

##### What is Goerli?  

- [ ]  A browser extension for interacting with Ethereum
- [x]  A public, proof-of-authority Ethereum test network
- [ ]  A JavaScript library for working with Ethereum
- [ ]  A set of tools for running a local Ethereum development blockchain
  
Hint: test network
         
Explanation: Goerli is a public, proof-of-authority Ethereum test network that is designed to be a stable and reliable environment for testing and deploying decentralized applications (dApps).

Sub Topics: No Sub-Topics
 

---

##### What is Ethers.js?  

- [ ]  A blockchain infrastructure and development platform
- [ ]  A set of tools for running a local Ethereum development blockchain
- [ ]  A local Ethereum test network
- [x]  A JavaScript library for working with Ethereum
  
Hint: library
         
Explanation: Ethers.js is a JavaScript library for working with the Ethereum blockchain.

Sub Topics: No Sub-Topics
 

---

##### What does the pragma solidity ^0.8.9; statement do in the smart contract code?  

- [ ]  It imports the hardhat/console.sol library
- [x]  It sets the Solidity compiler version to 0.8.9
- [ ]  It extends the ERC20 contract from the OpenZeppelin library
- [ ]  It defines a token contract called Token
  
Hint: NoHint
         
Explanation: It sets the Solidity compiler version to 0.8.9. Solidity files have to start with this pragma. It will be used by the Solidity compiler to validate its version.

Sub Topics: No Sub-Topics
 

---

##### What does the `external` modifier do in the transfer function?  

- [x]  It makes the function callable only from outside the contract
- [ ]  It makes the function callable only from within the contract
- [ ]  It logs the transfer information using the console.log function
- [ ]  It calls the transfer function from the ERC20 contract
  
Hint: external is synonymous to?
         
Explanation: The `external` modifier makes a function only callable from outside the contract.

Sub Topics: No Sub-Topics
 

---

##### How do you compile the smart contract code in this template?  

- [ ]  npm compile
- [ ]  npm install
- [x]  npx hardhat compile
- [ ]  npx hardhat
  
Hint: NoHint
         
Explanation: npx hardhat compile is used to compile the smart contract code.

Sub Topics: No Sub-Topics
 

---

##### What is the use of Makefile?  

- [x]  It provides a list of commands for working with the project
- [ ]  It compiles the smart contract code
- [ ]  It deploys the smart contract to the Ethereum network
- [ ]  It installs the project dependencies
  
Hint: NoHint
         
Explanation: A Makefile provides a number of useful commands for working with the project. For example, you can use the make compile command to compile the contract code. You can see the full list of commands by running make or make help.

Sub Topics: No Sub-Topics
 

---

##### What is the `await` keyword used for in the deploy script?  

- [x]  It is used to wait for a promise to be resolved
- [x]  It is used to pause the execution of the function until the asynchronous operation is completed
- [ ]  It is used to skip a promise before it gets resolved
- [ ]  It is used to connect to the Ethereum network
  
Hint: NoHint
         
Explanation: It is used to wait for a promise to be resolved and to handle asynchronous operations.It is used to pause the execution of the function until the asynchronous operation is completed

Sub Topics: No Sub-Topics
 

---

##### How does the deploy script save the contract's address and ABI to the frontend directory?  

- [ ]  It writes the values to a contract-address.json file
- [ ]  It saves the contract's artifacts to a Token.json file
- [ ]  It creates a typechain-types directory
- [x]  All of the above
  
Hint: saveFrontendFiles function
         
Explanation: The script saves the contract's address and ABI to the frontend directory using the saveFrontendFiles function. This function writes the contract's address and ABI to a contract-address.json file and saves the contract's artifacts to a Token.json file in the frontend directory.

Sub Topics: No Sub-Topics
 

---

##### What library is used to interact with the Ethereum network and deploy the contract in the deploy script?  

- [ ]  TypeScript
- [x]  Ethers.js
- [ ]  Hardhat
- [ ]  None of the above
  
Hint: Others are not libraries.
         
Explanation: Ethers.js is used to interact with the Ethereum network and deploy the contract in the deploy script

Sub Topics: No Sub-Topics
 

---

##### How do you access the contract address in the front-end of the DApp using Ethers.js?  

- [x]  Import the contract-addresses.json file and use the ethers.getContractAt method
- [ ]  Import the Token.json file and use the ethers.getContractAt method
- [ ]  Import the contract-addresses.json file and use the ethers.getContractFactory method
- [ ]  Import the Token.json file and use the ethers.getContractFactory method
  
Hint: contract-address.json
         
Explanation: We can access it by importing the contract-addresses.json file and use the ethers.getContractAt method

Sub Topics: No Sub-Topics
 

---

##### What does the deployed method do in the deploy script?  

- [ ]  It deploys the contract to the network
- [ ]  It saves the contract's artifacts to a file
- [x]  It waits for the contract deployment to be confirmed on the network
- [ ]  It logs the contract's address to the console
  
Hint: NoHint
         
Explanation: It waits for the contract deployment to be confirmed on the network

Sub Topics: No Sub-Topics
 

---

##### What does the saveFrontendFiles function do in the deploy script?  

- [x]  It saves the contract's address and ABI to the frontend directory
- [ ]  It deploys the contract to the network
- [ ]  It waits for the contract deployment to be confirmed on the network
- [ ]  It logs the contract's address to the console
  
Hint: NoHint
         
Explanation: This function writes the contract's address and ABI to a contract-address.json file and saves the contract's artifacts to a Token.json file in the frontend directory.

Sub Topics: No Sub-Topics
 

---

##### What is the fs.existsSync method used for in the deploy script?  

- [ ]  It is used to create a directory
- [ ]  It is used to copy a directory
- [x]  It is used to check if a directory exists
- [ ]  It is used to delete a directory
  
Hint: Does it exist?
         
Explanation: It is used to check if a directory exists

Sub Topics: No Sub-Topics
 
