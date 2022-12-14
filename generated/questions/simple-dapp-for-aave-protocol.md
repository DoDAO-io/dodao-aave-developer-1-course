## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Simple Dapp for Aave Protocol
 
 
---

##### What is the purpose of the IPriceOracleGetter contract imported in the Aave contract?  

- [x]  To get the price of a token in USD
- [ ]  To get the data of the Aave pool
- [ ]  To get the data of the user's reserve
- [ ]  To get the configuration of the reserve
  
Hint: NoHint
         
Explanation: The purpose of the IPriceOracleGetter contract imported in the Aave contract is to get the price of a token in USD.

Sub Topics: No Sub-Topics
 

---

##### What is the purpose of the supplyTokenAddress variable in the contract?  

- [ ]  It is used to store the address of the Aave pool contract
- [ ]  It is used to store the address of the ERC20 token that is being borrowed from the Aave pool
- [x]  It is used to store the address of the ERC20 token that is being supplied to the Aave pool
- [ ]  It is used to store the address of the Aave Oracle contract
  
Hint: ERC20 token
         
Explanation: It is used to store the address of the ERC20 token that is being supplied to the Aave pool.

Sub Topics: No Sub-Topics
 

---

##### What is the name of the function that is used to borrow tokens in the contract?  

- [ ]  getReserveData
- [ ]  supply
- [x]  borrow
- [ ]  getAssetPrice
  
Hint: Supply? Nah, definitely Borrow
         
Explanation: Borrow function is used to borrow tokens in the contract.

Sub Topics: No Sub-Topics
 

---

##### What is a proxy contract in Ethereum development?  

- [ ]  A contract that is deployed when a new version of the contract needs to be created
- [ ]  A contract that is deployed when the contract's bytecode needs to be updated
- [ ]  A contract that is deployed when the contract's state needs to be updated
- [x]  A special type of contract that acts as a middleman between the user and the actual contract
  
Hint: middleman
         
Explanation: A proxy contract in Ethereum development is a special type of contract that acts as a middleman between the user and the actual contract.

Sub Topics: No Sub-Topics
 

---

##### What is the advantage of using a proxy contract for contract upgrades?  

- [ ]  It allows the contract to be updated without affecting its address or its state
- [ ]  It allows the contract to be updated without requiring users to migrate their data
- [x]  Both of the above
- [ ]  None of the above
  
Hint: NoHint
         
Explanation: Ethereum provides a mechanism for upgrading contracts called proxy contracts. A proxy contract is a special type of contract that acts as a middleman between the user and the actual contract. The proxy contract has a reference to the actual contract, and it forwards calls and transactions to the actual contract. When the actual contract needs to be updated, the developer can simply deploy a new version of the contract and update the proxy contract to point to the new contract. This allows the contract to be updated without affecting its address or its state, and without requiring users to update their contract references or migrate their data.

Sub Topics: No Sub-Topics
 

---

##### What does the getNormalizedBalance function do?  

- [ ]  Returns the USDC balance of the contract
- [x]  Returns the normalized balance of a token for the specified provider and account
- [ ]  Returns the USDC balance of the user
- [ ]  Returns the address of the USDC contract
  
Hint: NoHint
         
Explanation: It returns the normalized balance of a token for the specified provider and account.

Sub Topics: No Sub-Topics
 

---

##### What is the purpose of the MintUSDC component?  

- [x]  To mint USDC tokens and transfer them to the user's account
- [ ]  To transfer USDC tokens from a contract address to the user's account
- [ ]  To transfer USDC tokens from the user's account to a contract address
- [ ]  To mint USDC tokens and transfer them to the contract address
  
Hint: mint and transfer
         
Explanation: The purpose of the MintUSDC component is to mint USDC tokens and transfer them to the user's account.

Sub Topics: No Sub-Topics
 

---

##### What is the purpose of the IERC20__factory.connect method?  

- [ ]  It creates a new instance of the IERC20 contract
- [ ]  It creates a new provider using window.ethereum
- [x]  It connects the IERC20 contract to the Ethereum network
- [ ]  It connects the Dapp component to the Ethereum network
  
Hint: connect
         
Explanation: It connects the IERC20 contract to the Ethereum network.

Sub Topics: No Sub-Topics
 

---

##### How does the Supply component calculate the amount of LINK that can be minted from a USDC supply?  

- [ ]  It divides the supply amount by the link price
- [ ]  It multiplies the supply amount by the link price
- [ ]  It divides the supply amount by the USDC threshold
- [x]  It multiplies the supply amount by the USDC threshold
  
Hint: multiply
         
Explanation: It multiplies the supply amount by the USDC threshold.

Sub Topics: No Sub-Topics
 

---

##### What is the purpose of the updateContractBalance function?  

- [ ]  To update the USDC balance of the user
- [x]  To update the USDC balance of the contract
- [ ]  To update the balance of the user for all supported tokens
- [ ]  To update the balance of the contract for all supported tokens
  
Hint: USDC token
         
Explanation: The function updates the USDC balance of the contract.

Sub Topics: No Sub-Topics
 

---

##### What is the purpose of the getTokenContract function?  

- [ ]  To get the contract address of the specified token
- [x]  To get the contract instance of the specified token
- [ ]  To get the contract balance of the specified token
- [ ]  To get the contract owner of the specified token
  
Hint: NoHint
         
Explanation: It's purpose is to get the contract instance of the specified token.

Sub Topics: No Sub-Topics
 

---

##### What is the value of normalizedBalance after the following code executes? ```const userTokenBalance = BigNumber.from("5000000000"); const normalizedBalance = userTokenBalance.div( BigNumber.from("1000000").toString() ); ```  

- [ ]  5
- [ ]  500
- [x]  5000
- [ ]  5000000
  
Hint: divide
         
Explanation: 5000000000/1000000 = 5000

Sub Topics: No Sub-Topics
 

---

##### What is the purpose of the FaucetService class?  

- [ ]  To provide users with access to testnet Aave faucets
- [ ]  To provide users with access to mainnet Aave faucets
- [x]  To provide users with access to Aave faucet contract instances
- [ ]  To provide users with access to Aave faucet contract addresses
  
Hint: NoHint
         
Explanation: The purpose of the FaucetService class is to provide users with access to Aave faucet contract instances.

Sub Topics: No Sub-Topics
 

---

##### What is the purpose of the createPoolSlice function?  

- [ ]  To create a new instance of the Pool class
- [ ]  To create a new instance of the LendingPool class
- [ ]  To create a new instance of the UiPoolDataProvider class
- [x]  To create a new Map containing pool data
  
Hint: NoHint
         
Explanation: To create a new Map containing pool data.

Sub Topics: No Sub-Topics
 

---

##### What is the value of the marketInfo.marketTitle constant?  

- [x]  Ethereum Görli
- [ ]  Ethereum Rinkeby
- [ ]  Ethereum Mainnet
- [ ]  Ethereum Kovan
  
Hint: The test network we used.
         
Explanation: Ethereum Görli is the value of the marketInfo.marketTitle constant.

Sub Topics: No Sub-Topics
 
