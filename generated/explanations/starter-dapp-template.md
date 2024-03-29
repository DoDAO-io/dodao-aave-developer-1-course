## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Starter-DApp-Template
 
 **Introduction**        
## Dapps
The main components of a blockchain Dapp (decentralized application) are:

1. **Smart contracts**: Many Dapps use smart contracts, which are self-executing contracts with the terms of the agreement between buyer and seller being directly written into lines of code. These contracts allow for transactions to be carried out automatically and transparently, without the need for intermediaries.

2. **Front-end user interface**: A Dapp has a user interface that allows users to interact with the Dapp and carry out transactions. This interface can be a web-based application or a mobile app.

3. **Blockchain network**: A blockchain network to which the smart contract is deployed e.g.  Ethereum Mainnet, Polygon, Arbitrum etc.

## Creating an Dapp
Creating and deploying Smart Contracts, as well as interacting with them, has not been standardized across the ecosystem. This means that every project has to spend extra time developing their own setup, rather than being able to use ones that have already been created. Standardization would save a lot of time and allow new projects to get started much faster.

## DoDAO Dapp template
As, creating and deploying smart contracts can be a bit daunting, we've created a starter template using HardHat that makes it easy to deploy smart contracts. Plus, our deploy scripts automatically save the deployed smart contract's address in the front end code so that the front end can reference it later on.

We also use generated typescript files, using which interacting with Smart Contracts is as simple as calling a JavaScript function.
  
[Here](https://github.com/DoDAO-io/dodao-simple-contract-template) is the link to the template. 
 **Starter App**        
## Simple ERC20 Starter App
Our template includes a simple application that we can use to create and deploy an ERC20 contract. We can then use the UI to interact with the Smart Contract. The frontend application of the template looks like this:

![starter-template-image](https://raw.githubusercontent.com/DoDAO-io/dodao-aave-developer-1-course/main/images/starter-template.png)

The deployer can then transfer the tokens to whichever address they like.
 
 **Stack Overview**        
#### The stack/tools used in the template
* Solidity (To write the smart contract) 
* Hardat (Build, test and deployment framework) 
* React (Build the frontend) 
* Ethers (To interact with the blockchain and the smart contract) 
* MetaMask (Wallet browser extension) 
* Alchemy (Node provider)
#### Overview of the stack
* [Solidity](https://docs.soliditylang.org/en/v0.8.17/) is a programming language for writing smart contracts that run on the Ethereum platform. It is a high-level language that is easy to read and write, and it is compiled, meaning that the code is converted into a format that is executable by the Ethereum Virtual Machine.  Solidity is a powerful and versatile language for creating smart contracts.
* [Hardhat](https://hardhat.org/) is a set of tools that facilitates developers in running a local Ethereum development blockchain, writing Solidity smart contract code, running smart contract tests, and debugging Solidity code, all without dealing with live Ethereum blockchain networks. You'll use Hardhat to run your own local Ethereum test network.
* [React](https://reactjs.org/) is a JavaScript library for building user interfaces. It is designed to make it easy for developers to create complex and dynamic user interfaces,  by breaking them down into small, reusable components. React allows developers to efficiently update the user interface in response to user input or changes in data.  It is widely used by web and mobile developers to create interactive and user-friendly applications.
* [Ethers.js](https://docs.ethers.org/v5/) is a JavaScript library for working with the Ethereum blockchain.  It provides a simple and intuitive interface for developers to build applications that interact with Ethereum, including support for working with smart contracts, accounts, and transactions.  Ethers.js is widely used by developers building Ethereum applications.
* [MetaMask](https://docs.metamask.io/guide/) is a browser extension that allows users to interact with the Ethereum blockchain.  It provides a secure and user-friendly way to manage Ethereum accounts, sign transactions, and interact with decentralized applications (DApps) in the browser.  MetaMask also allows users to access the Ethereum mainnet and test networks, such as Goerli, making it easy to switch between networks and test contracts without the need to run a full Ethereum node.
* [Alchemy](https://www.alchemy.com/) is a blockchain infrastructure and development platform that provides developers with tools and services for building and deploying decentralized applications (dApps) on Ethereum and other networks.  Alchemy offers a suite of nodes, which are nodes on the Ethereum network that are managed and maintained by the Alchemy team.  These nodes provide developers with a reliable and secure connection to the Ethereum network, allowing them to easily interact with dApps and other contracts on the network.
* [Goerli](https://goerli.net/) is a public, proof-of-authority Ethereum test network that is designed to be a stable and reliable environment for testing and deploying decentralized applications (dApps).  By using Goerli, developers can test their dApps and contracts in a real-world environment without risking any real Ether or other assets.  This allows developers to ensure that their dApps are functioning properly before deploying them to the main Ethereum network.
* To complete the tutorial, you will need to use the [Git](https://git-scm.com/) command line interface (CLI) tool to download the example code from GitHub. You will also need to install and use Node.js and/or Yarn to build, compile, and run the smart contract and frontend Dapp. You will use a terminal window to run the CLI tools and manage the project.
 
 **Template Setup**        
### Setup General steps to build a web3 Dapp
To create a web3 DApp using Solidity, Hardhat, React, Ethers.js, MetaMask, and the Alchemy node on the Goerli test network, you will need to use the following steps:
* Set up a development environment for building Ethereum DApps, including installing Node.js, yarn or npm, and the required dependencies for Solidity, Hardhat, React, and Ethers.js. 
* Write a smart contract for the DApp using Solidity. This will involve defining the contract's state variables and functions, and testing them using Hardhat. 
* Compile the contract using Hardhat and solc, and deploy it to the Goerli test network using the Alchemy node. 
* Create the front-end for the DApp using React, and use Ethers.js to interact with the deployed contract. 
* Test the DApp using a testing framework like Mocha or Chai, to ensure that it is working as expected. 
* Publish the DApp to a hosting platform like GitHub Pages or Netlify, and use MetaMask to access it on the web.

Once the DApp is published, users will be able to interact with the contract on the Goerli test network using their MetaMask-enabled browser,  and they will be able to use the DApp's user interface to send and receive tokens, check their balances, and view the contract's transaction history.

Now, Let's take a deep dive into the template. But before looking at the code, let's setup our metamask wallet and alchemy account.

### MetaMask Installation & Configuration

* To install MetaMask, first visit the MetaMask website (https://metamask.io/) and click the "Get MetaMask" button.  This will take you to the page for the MetaMask extension on the Chrome web store (https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn ), where you can click "Add to Chrome" to install the extension.  
* Once the extension is installed, you will see the MetaMask icon appear in your browser's toolbar. Clicking on the icon will open the MetaMask pop-up window, where you can create a new account or import an existing one.
* After creating an account, you will need to configure MetaMask to connect to the Ethereum network. To do this, click on the network dropdown in the top-left corner of the MetaMask window and select the network you want to connect to (e.g. "Main Ethereum Network" for the mainnet, or "Goerli Test Network" for the Goerli test network).  You can also add custom networks by clicking the "Custom RPC" option and entering the network's URL.
* Once you have configured MetaMask to connect to the desired network, you can use it to manage your Ethereum accounts, sign transactions, and interact with decentralized applications.  You can also use MetaMask to switch between networks and test contracts without the need to run a full Ethereum node.

### Getting access to Goerli Test network using Alchemy

* To get access to an Alchemy node on the Goerli test network, you will first need to create an account on the Alchemy website (https://alchemy.com/). 
* Once your account is created, you will be able to log in to the Alchemy dashboard and access the network settings for the Goerli test network.  From there, you can generate an API key that you can use to connect to the Alchemy node.
* To connect to the Alchemy node using the generated API key, you will need to use a library or tool that supports the Alchemy API. For example, if you are using the Web3.js library, you can connect to the Alchemy node by using the Web3.eth.alchemy method, passing in the API key as a parameter.
* Once you are connected to the Alchemy node, you can use it to interact with the Goerli test network, including sending transactions and deploying and calling smart contracts. You can also use the Alchemy dashboard to monitor your node's performance and track your usage of the Alchemy API.

### Template Code Setup

Now, let's use the template code. To use the code in the DoDAO-io/dodao-simple-contract-template GitHub repository, you will need to have Node.js and npm installed on your computer. Once you have these tools installed, you can follow these steps to use the template code:
* Download or clone the repository to your local computer using git:
  ```
  git clone https://github.com/DoDAO-io/dodao-simple-contract-template.git
  ```
* Navigate to the root directory of the repository and install the project dependencies using npm:
  ```
  npm install
  ```

* Compile the smart contract code by running the following command:
  ```
  npx hardhat compile
  ```

* Deploy the smart contract to the Goerli network by running the deploy script:
  ```
  npx hardhat run scripts/deploy.ts --network goerli
  ```

* Once the contract has been deployed, you can interact with it using the frontend directory. This directory contains a simple web application built with React that allows you to send and receive tokens using the deployed contract. To run the frontend, navigate to the frontend directory and run the following commands:
  ```
  cd frontend
  npm install
  npm start
  ```

* The frontend should now be running on your local computer. You can access it by visiting http://localhost:3000 in your web browser.
* In addition to the steps above, the template also includes a Makefile that provides a number of useful commands for working with the project. For example, you can use the make compile command to compile the contract code. You can see the full list of commands by running make or make help.
 
 **Smart Contract Explanation & Deployment**        
### Smart Contract
Its time to have a look on the smart contract.

```solidity
//SPDX-License-Identifier: UNLICENSED
// Solidity files have to start with this pragma. // It will be used by the Solidity compiler to validate its version. pragma solidity ^0.8.9;
// We import this library to be able to use console.log import "hardhat/console.sol"; import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
// This is the main building block for smart contracts. contract Token is ERC20 {
    /**
    * Contract initialization.
    */
    constructor() ERC20("My Hardhat Token", "MHT") {
        _mint(msg.sender, 1000000);
    }

    function decimals() public view virtual override returns (uint8) {
        return 2;
    }

    /**
    * A function to transfer tokens.
    *
    * The `external` modifier makes a function *only* callable from outside
    * the contract.
    */
    function transfer(
        address to,
        uint256 amount
    ) public virtual override returns (bool) {
        console.log(
            "Transferring from %s to %s %s tokens",
            msg.sender,
            to,
            amount
        );

        return super.transfer(to, amount);
    }
} 
```

The above smart contract is written in Solidity and defines a token contract called Token. The contract extends the ERC20 contract from the OpenZeppelin library, which provides a standard interface for ERC20 token contracts.

The contract's constructor function is called when the contract is deployed, and it initializes the contract with the name "My Hardhat Token" and the symbol "MHT".  It also uses the _mint function from the ERC20 contract to mint 1,000,000 tokens and transfer them to the contract's deployer.

The contract also defines a decimals function, which returns the number of decimal places used by the token. In this case, the function returns 2, indicating that the token uses 2 decimal places.
The contract also defines a transfer function, which allows users to transfer tokens from one account to another. The function logs the transfer information using the console.log function from the hardhat/console.sol library, and then calls the transfer function from the ERC20 contract using the super keyword to actually perform the transfer. This function is marked with the external modifier, which makes it only callable from outside the contract.

### Deploying the smart contract 

To deploy our smart contract, we used the following deploy script.

```typescript

import { artifacts, ethers } from "hardhat"; import { Token } from "./../typechain-types/contracts/Token";

async function main() {
  const Token = await ethers.getContractFactory("Token");
  const token = await Token.deploy();
  await token.deployed();

  console.log("Token address:", token.address);

  // We also save the contract's artifacts and address in the frontend directory
  saveFrontendFiles(token);
}
// We recommend this pattern to be able to use async/await everywhere // and properly handle errors. main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
// This is a script for deploying your contracts. You can adapt it to deploy // yours, or create new ones.
const path = require("path");
function saveFrontendFiles(token: Token) {
  const fs = require("fs");
  const contractsDir = path.join(
    __dirname,
    "..",
    "frontend",
    "src",
    "contracts"
  );

  if (!fs.existsSync(contractsDir)) {
    fs.mkdirSync(contractsDir);
  }

  fs.writeFileSync(
    path.join(contractsDir, "contract-address.json"),
    JSON.stringify({ Token: token.address }, undefined, 2)
  );

  const TokenArtifact = artifacts.readArtifactSync("Token");

  fs.writeFileSync(
    path.join(contractsDir, "Token.json"),
    JSON.stringify(TokenArtifact, null, 2)
  );

  fs.cpSync(
    path.join(__dirname, "..", "typechain-types"),
    path.join(
      __dirname,
      "..",
      "frontend",
      "src",
      "contracts",
      "typechain-types"
    ),
    { recursive: true }
  );
}
main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });

```

The above deploy script is written in TypeScript and is used to deploy the Token smart contract defined in Token.sol to an Ethereum network.  The script uses the Ethers.js library to interact with the Ethereum network and deploy the contract.

The script first imports the required dependencies, including the Token contract from the compiled Token.sol contract file and the ethers object from the Hardhat library.

Next, the script defines a main function, which is the entry point for the script. This function first uses the ethers.getContractFactory function to create a contract factory for the Token contract,  and then uses the deploy method on the contract factory to deploy the contract to the network. The deployed method is called on the contract instance to wait for the deployment to be confirmed on the network.

The script then logs the contract's address to the console using the console.log function, and then saves the contract's address and ABI to the frontend directory using the saveFrontendFiles function.  This function writes the contract's address and ABI to a contract-address.json file and saves the contract's artifacts to a Token.json file in the frontend directory.

Overall, this deploy script provides a simple and straightforward way to deploy the Token contract to an Ethereum network using Ethers.js. It also saves the deployed contract's address and ABI to the frontend directory,  making it easy to access these values in the front-end code.
 
 **Frontend Explanation**        
### Frontend 

The frontend of the template is a simple web application built with React that allows users to interact with the Token smart contract that is included in the template. The frontend code is located in the frontend directory of the repository, and is structured as follows:

* `src/contracts`: This directory contains the contract artifacts and address information that is needed to interact with the contract.  The contract artifacts are automatically generated by the hardhat tool when the contract is compiled, and the contract address is saved in a contract-address.json file by the deploy script.

* `src/components`: This directory contains the React components that make up the user interface of the frontend. The main components are the App component, which is the root component of the application,  and the Token component, which is used to display and interact with the contract.

* `src/index.tsx`: This is the entry point of the frontend application. It is responsible for rendering the App component to the page and initializing the ethers.js library, which is used to interact with the contract.

To use the frontend, you will need to have the Token contract deployed to the Ethereum network, and the contract address and artifacts will need to be saved in the src/contracts directory.  Once this is done, you can run the frontend by navigating to the frontend directory and running the following commands:

```
cd frontend 
npm install 
npm start 
```

The frontend should now be running on your local computer, and you can access it by visiting `http://localhost:3000` in your web browser. Once the frontend is running, you can start interacting with it.

### Benefits of using Typescript

As you can see, we preferred using Typescript in our code instead of Javascript. There are several benefits to using generated typings (also known as type definitions or type declarations) in TypeScript.  These benefits include the following:

* **Improved code correctness**: Generated typings provide type information for the objects and functions in your code, allowing the TypeScript compiler to catch type errors at compile time, rather than at runtime.  This can help you avoid runtime errors and improve the overall correctness of your code.

* **Better code completion and documentation**: Generated typings can provide detailed type information for your code, allowing your code editor or IDE to provide accurate code completion suggestions and inline documentation.  This can help you write code more quickly and understand the APIs you are using more easily.

* **Improved code maintainability**: Generated typings can help you refactor your code with confidence, by providing type information for the objects and functions in your code.  This can make it easier to update your code without breaking existing functionality.

* **Easier integration with external libraries**: Many popular JavaScript libraries, such as React and lodash, provide generated typings that can be used with TypeScript.  This allows you to use these libraries in your TypeScript code with full type information, making it easier to integrate them into your project.

Overall, using generated typings in TypeScript can help you write safer, more maintainable, and more robust code, and can make it easier to integrate your code with external libraries and frameworks.

### How contract address is saved in contract-addresses.jon and how we access it in Frontend using ethers.js

In a typical Ethereum DApp, the contract address is saved in a file called `contract-addresses.json`, which is generated during the contract deployment process. This file is typically located in the root directory of the DApp's project, and it contains the contract's address, as well as any other relevant deployment information, such as the contract's ABI and the network it was deployed to.
To access the contract address in the DApp's front-end using Ethers.js, you will first need to import the contract-addresses.json file and use it to create a new instance of the Contract class from Ethers.js, passing in the contract's ABI and the contract address as parameters. For example, the code for creating a contract instance might look like this:

```typescript
import contractAddress from "@contracts/contract-address.json";
import { ethers } from "ethers";
// Create a new contract instance 
this._token = new ethers.Contract(
      contractAddress.Token, // The contract address
      TokenArtifact.abi,  // The contract ABI
      this._provider.getSigner(0)
    ) as Token;
``` 

Once you have created a contract instance, you can use it to call the contract's functions and access its state variables.  For example, you can use the contract instance to call the contract's balanceOf function to check the balance of a given account, or to call its transfer function to send tokens to another account. 

By storing the contract address in contract-addresses.json and importing it in the front-end using Ethers.js, you can ensure that the DApp is always using the correct contract address,  regardless of which network it is deployed to or which version of the contract is currently active. This makes it easy to manage multiple contract deployments  and to switch between different networks without having to manually update the contract address in the front-end code.
 
 
