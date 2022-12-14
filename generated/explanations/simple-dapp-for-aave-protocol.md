## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Simple Dapp for Aave Protocol
 
 **Introduction**        
### Problem Statement Aave is a decentralized finance (DeFi) platform that offers users the ability to lend and borrow cryptocurrency. The platform specializes in overcollateralized loans, where borrowers must deposit a higher value of cryptocurrency than the amount they wish to borrow. This protects lenders from potential losses due to loan defaults, and allows the Aave protocol to liquidate the collateral if it decreases significantly in value.
Our goal is to build a simple example of how to build a Dapp that allows users to interact with the Aave protocol on the Ethereum blockchain and demonstrate how you can further interact with Aave and build applications on top of it. 
So, the idea for this DApp is to allow users to receive undercollateralized loan from Aave. For this, we will create a DApp that works on top of Aave smart contracts and adds part of the collateral from our side so that the user receives more loan from Aave than the amount of collateral he has deposited and Aave is still providing overcollateralized loan, so a win-win for both sides. The amount of collateral we top up is 50% of the amount eligible for the user.  So the user supplies USDC tokens and receives LINK tokens in return based on the USDC threshold in Aave i.e. 85%. Our contract then tops up the user's LINK amount by 50% of the eligibility.
Here is a screenshot of the application:

To create the DApp we used the [starter dapp template](https://github.com/DoDAO-io/dodao-simple-contract-template) that we built in the previous chapter. 
### Template Overview
* Solidity (To write our smart contract) * Hardat (build, test and deployment framework) * React (Create our frontend) * Ethers (web3 library for interacting with the blockchain and our smart contract) * MetaMask (Wallet browser extension) * Alchemy (node provider)
The starter template uses the above stack/tools. So, before moving forward make sure to have the initial setup ready following the previous chapter.
Now, let's move on to the code setup for the DApp which we will discuss in this chapter. You can find the complete code [here](https://github.com/DoDAO-io/aave-call-smart-contracts).
 
 **Code Setup**        
To use the code in the DoDAO-io/aave-call-smart-contracts GitHub repository, you will need to have Node.js and npm installed on your computer. Once you have these tools installed, you can follow these steps to setup the code:
* Download or clone the repository to your local computer using git:
  ```
  git clone https://github.com/DoDAO-io/aave-call-smart-contracts.git 
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
  npx hardhat run scripts/compile.ts
  npx hardhat run scripts/old-deploy.ts --network goerli
  ```

* We use an upgradable smart contract, so to deploy it after making changes you can use:
  ```
  npx hardhat run scripts/update.ts --network goerli
  ```

* Once the contract has been deployed, you can interact with it using the frontend directory. This directory contains a simple web application built with React that allows you to send and receive tokens using the deployed contract. To run the frontend, navigate to the frontend directory and run the following commands:
  ```
  cd frontend
  npm install
  npm start
  ```
  
* The frontend should now be running on your local computer. You can access it by visiting `http://localhost:3000` in your web browser.
* In addition to the steps above, the template also includes a Makefile that provides a number of useful commands for working with the project. For example, you can use the make compile command to compile the contract code. You can see the full list of commands by running make or make help.
 
 **Code Explanation**        
### Smart Contract
```solidity
// SPDX-License-Identifier: MIT pragma solidity ^0.8.10; pragma abicoder v2;
import "@aave/core-v3/contracts/interfaces/IPool.sol"; import "@aave/core-v3/contracts/interfaces/IAaveOracle.sol"; import "@aave/core-v3/contracts/interfaces/IPriceOracleGetter.sol"; import "@aave/core-v3/contracts/misc/AaveOracle.sol"; import "@aave/core-v3/contracts/protocol/libraries/configuration/ReserveConfiguration.sol"; import "@aave/core-v3/contracts/protocol/libraries/types/DataTypes.sol"; import "@openzeppelin/contracts/token/ERC20/IERC20.sol"; import "hardhat/console.sol";
contract Aave {

    // Storage Variables
    address public borrowTokenAddress = 0x07C725d58437504CA5f814AE406e70E21C5e8e9e;
    address public supplyTokenAddress = 0xA2025B15a1757311bfD68cb14eaeFCc237AF5b43;
    address public aavePoolAddress = 0x368EedF3f56ad10b9bC57eed4Dac65B26Bb667f6;
    address public dataProviderAddress = 0x9BE876c6DC42215B00d7efe892E2691C3bc35d10;
    address public aaveOracleAddress = 0x5bed0810073cc9f0DacF73C648202249E87eF6cB;
    using ReserveConfiguration for DataTypes.ReserveConfigurationMap;


    function supply(uint _userAmount) public returns (bool) {

        // Top up the collateral to double
        uint _total = _userAmount * 2;


        // Transfer _useramount from user to contract
        IERC20(supplyTokenAddress).transferFrom(msg.sender, address(this), _userAmount * 1000000);

        // Get the reserveData as that contains the threshold i.e. the max amount of assert that can be bought against USDC
        DataTypes.ReserveData memory reserveData = IPool(aavePoolAddress).getReserveData(supplyTokenAddress);

        // prices are returned in USD with 6 decimal places
        uint256 linkPrice = IPriceOracleGetter(aaveOracleAddress).getAssetPrice(borrowTokenAddress);

        // normalize the amount and reduce the six decimal digits
        uint256 linkPriceInUSDC = linkPrice / 100000000;

        // threshold is returned as 8500, so we need to normalize it
        uint256 threshold = reserveData.configuration.getLiquidationThreshold();

        // Supply _total i.e. double the users amount to Aave pool
        IERC20(supplyTokenAddress).approve(aavePoolAddress, _total * 1000000);
        IPool(aavePoolAddress).supply(supplyTokenAddress, _total * 1000000, address(this), 0);

        // divide by 10000 as the threshold is 8500 i.e. 85%
        uint256 userUSDCBorrowAmount = (_userAmount * threshold) / 10000 ;

        // USDC amount to be used for borrow - we borrow 1.5 times the max user limit
        uint256 usdcBorrowAmount = (userUSDCBorrowAmount * 3) / 2 ;

        // USDC amount to be used for borrow - we borrow 1.5 times the max user limit
        uint256 numberOfLinkTokens = usdcBorrowAmount / linkPriceInUSDC ;

        console.log("Trying to borrow %s link after adding %s USDC. Users eligible borrow amount is", numberOfLinkTokens, _total, userUSDCBorrowAmount);

        // Borrow the LINK tokens from Aave
        IPool(aavePoolAddress).borrow(borrowTokenAddress, numberOfLinkTokens * 1 ether, 2, 0, address(this));


        // Transfer LINK to user
        IERC20(borrowTokenAddress).transfer(msg.sender, numberOfLinkTokens * 1 ether);

        return true;
    }

}
```
The Aave.sol contract has one main function, supply(), which allows users to supply collateral to the Aave protocol and use it to borrow other assets. The supply() function takes in an input, _userAmount, which specifies the amount of collateral that the user wants to supply. The function then uses this input to do the following: Transfer the user-specified amount of collateral from the user's account to the contract's account.
Use the supplied collateral to borrow a specified amount of another asset. Transfer the borrowed asset to the user's account. The supply() function uses various interfaces and libraries to interact with other contracts on the Aave protocol. For example, the IPool interface is used to interact with the Aave pool, which is where users can supply their collateral and borrow assets. The IERC20 interface is used to interact with the ERC-20 tokens used on the protocol. The AaveOracle contract is used to get the current price of the asset being borrowed.
At the top of the contract, several other contracts are imported. These include contracts for interfacing with the Aave protocol, a contract for handling ERC20 tokens, and a contract for logging messages to the console. The contract has one public function called supply. This function takes a single argument, an unsigned integer called _userAmount. The function returns a single boolean value indicating whether the function executed successfully. The function first calculates the total amount to be supplied to the Aave pool by multiplying the user's supplied amount by 2. It then transfers the user's supplied amount from the user's address to the contract's address using the transferFrom method on the IERC20 contract. Then it retrieves the reserve data for the supply token using the getReserveData method on the IPool contract. This data contains the maximum amount of assets that can be bought against the USDC token. Then uses the getAssetPrice method on the IPriceOracleGetter contract to get the price of the borrow token in USD. This price is then divided by 100000000 to normalize it and remove the extra decimal places. Then the function calculates the user's eligible borrow amount by multiplying the user's supplied amount by the liquidation threshold from the reserve data, and dividing that result by 10000. This borrow amount is then multiplied by 1.5 to get the total amount of USDC to be used for borrowing. Then it calculates the number of LINK tokens to be borrowed by dividing the USDC borrow amount by the normalized price of the borrow token in USDC. This value is then logged to the console. The function then uses the approve and borrow methods on the IPool contract to borrow the calculated number of LINK tokens. The borrowed tokens are then transferred to the user's address using the transfer method on the IERC20 contract.
### Update.ts
The most important behavior of this file is that it upgrades an instance of the deployed contract on the Ethereum blockchain. The code uses the hardhat and ethers libraries to connect to the network and interact with the contract, and it uses the upgradeProxy method from the upgrades module to upgrade the contract. This allows the contract's bytecode to be updated without affecting its state or its address on the blockchain.
Contract upgrades are a common practice in Ethereum development. As smart contracts are immutable and cannot be modified once deployed, developers must create new versions of their contracts when they want to make changes to the contract's behavior. However, simply deploying a new contract would require users to update their contract references and migrate their data to the new contract.
To avoid this problem, Ethereum provides a mechanism for upgrading contracts called proxy contracts. A proxy contract is a special type of contract that acts as a middleman between the user and the actual contract. The proxy contract has a reference to the actual contract, and it forwards calls and transactions to the actual contract. When the actual contract needs to be updated, the developer can simply deploy a new version of the contract and update the proxy contract to point to the new contract. This allows the contract to be updated without affecting its address or its state, and without requiring users to update their contract references or migrate their data.
In the code above, the upgradeProxy method is used to upgrade the contract by deploying a new version of the contract and updating the proxy contract to point to the new contract. This allows the contract to be updated without affecting its address or its state, and without requiring users to update their contract references or migrate their data.
 
 **Helper Components**        
### PoolSlice.ts
The code imports several modules from the @aave/contract-helpers package, which provides a set of functions that make it easier to work with the Aave protocol, a decentralized lending and borrowing platform built on the Ethereum blockchain. The code defines an enum called ChainId, which lists several different Ethereum networks, including mainnet, ropsten, rinkeby, and goerli.
The code then defines an object called marketInfo that contains information about the Ethereum Görli network. This object includes the chainId of the Görli network, as well as the addresses of various contracts that are used by the Aave protocol on that network.
The code also defines an interface called SupplyActionProps that describes the shape of an object that is passed to a function called createPoolSlice. This function takes an account and a provider as arguments and returns an object with several methods for interacting with the Aave protocol. One of these methods, getPool, returns an instance of the Pool class from the @aave/contract-helpers package, which provides functions for working with Aave pools. Another method, getPoolData, uses the UiPoolDataProvider class from the @aave/contract-helpers package to retrieve data about an Aave pool.
Overall, this code provides a set of tools for working with the Aave protocol on the Ethereum Görli network.
### ContractsHelper.ts
This code provides a set of utility functions for working with the USDC and Link ERC-20 tokens on the Ethereum network. The getTokenContract function allows you to obtain an instance of the IERC20__factory interface connected to the USDC or Link contract, depending on the tokenType parameter passed to the function. This instance can be used to interact with the contract and perform various operations, such as checking a user's balance or transferring tokens.
The getNormalizedBalance function provides a convenient way to retrieve a user's token balance and convert it to a human-readable format. It does this by dividing the user's balance by the appropriate constant value (either 1,000,000 for USDC or 1,000,000,000,000,000,000 for Link), and returning the result as a BigNumber object. This allows you to easily display the user's balance in your application without worrying about the underlying details of how the balance is represented on the blockchain.
 
 **Main Components**        
### DApp.tsx
This is the main React component of our app that provides a user interface for interacting with the Aave protocol. The component connects to the user's Ethereum wallet, initializes the Aave contract, and polls the user's balance to keep it updated. It also provides a way for users to supply assets to Aave pools and to mint USDC tokens.
The component uses the @components/aave/MintUSDC and @components/aave/Supply components to render the user interface. It also imports the ConnectWallet component, which displays a message asking the user to connect their wallet if one is not detected. The component also imports the TransactionErrorMessage and WaitingForTransactionMessage components, which are used to display messages to the user if there is an error sending a transaction or if the component is waiting for a transaction to be processed.
The Dapp component uses the ethers library to connect to the Ethereum network and interact with the Aave contract. It also uses the typechain-types package to access the types and artifacts for the Aave contract. The component maintains its state using the React.Component class's state property, and it updates the user's balance by polling the Aave contract. The component also provides several methods for working with the Aave contract, including mintUSDC, aaveSupply, and getBalance.
Overall, this code provides a user interface for interacting with the Aave protocol on the Ethereum blockchain. It allows users to supply assets to Aave pools and to mint USDC tokens, and it provides a way to view the user's balance and transaction history.
### MintUSDC.tsx
It is a React component called "MintUSDC" that allows a user to mint USDC tokens and transfer them to a contract. The component has two buttons, one to mint 10K USDC tokens to the user's account and the other to transfer 2K USDC tokens to the contract. The component also displays the user's and contract's current USDC balances.
The component uses the getTokenContract function from the contractsHelper module to get the USDC token contract and the createPoolSlice function from the aave/poolSlice module to create a pool slice instance. The mintOneUSDC function is called when the user clicks the "Mint 10K USDC" button and it uses the pool slice instance to mint 10K USDC tokens to the user's account. The transferUSDCToContract function is called when the user clicks the "Transfer 2K USDC" button and it uses the USDC token contract to transfer 2K USDC tokens to the contract's address. Both functions also update the user's and contract's USDC balances by calling the updateUserUSDCBalance and updateContractBalance functions respectively. These functions use the getNormalizedBalance function from the contractsHelper module to get the user's and contract's normalized USDC balances.
### Supply.tsx
The code is a React component called "Supply" that allows users to supply USDC to the Aave lending protocol and receive LINK in return. It uses several helper functions from the "@components/helpers/contractsHelper" module to get information about the user's account and the state of the Aave protocol. It also imports the createPoolSlice function from the "@components/aave/poolSlice" module to get information about the Aave reserve pools.
It takes in two props: an account string representing the user's Ethereum address, and a provider object that allows the component to interact with the Ethereum network.
This component has several state variables to track the user's account, the contract's USDC balance, the amount of USDC being supplied, the current USDC threshold, the current LINK price, and the amount of mintable and top-up LINK. The component also has several functions to update these state variables, such as updateUserLINKBalance, getBalance, and updateReserveInfo.
The component has an input field where the user can enter the amount of USDC they want to supply, and a button to trigger the aaveSupply function. This function connects to the Aave contract, approves the transfer of USDC from the user's account to the contract, and calls the contract's supply function with the specified amount of USDC. After the transaction is complete, the component updates the contract's USDC balance and the user's LINK balance.
The component also has a refreshPage function that reloads the page, and a calculateLinks function that calculates the amount of mintable and top-up LINK based on the current state of the Aave protocol. This information is displayed to the user in the component's UI.
 
 
