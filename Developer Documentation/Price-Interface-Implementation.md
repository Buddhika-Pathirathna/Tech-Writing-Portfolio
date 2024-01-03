# Invoke Price Functions

This section explains how to implement the price interface in JavaScript code.
<br><br>
We will use [`IFtsoRegistry.sol`](#IFtsoRegistry.sol) interface to generate the contract code.

## Implement the Interface to Utilize Methods
We will implement a JavaScript code to interact with the smart contract using the ethers.js library. The code will initially connects the blockchain network, create a contract instance and then call the required functions to get price details.

IFtsoRegistry.sol Interface contains two methods to retrieve supported symbols and retrieve Current Price With Decimals.
Below

### Import Ethers Library
Import ethers.js package to facilitate the interaction with the blockchain.

```
const ethers = require("ethers");
```

### Add Network Connection Provider

Instantiate the *JsonRpcProvider* which connects with the blockchain network.

Add the your Blockchain Network URL Eg: Your Ethereum Node URL

```
const { JsonRpcProvider } = require('ethers');
const rpcUrl = 'https://example.com/ethereum/rpc';
const provider = new JsonRpcProvider(rpcUrl);
```
- Extract the JsonRpcProvider from the imported ethers library 
- Creates an instance of it using a specified Ethereum RPC (Remote Procedure Call) URL. 
- This URL is the connection to an Ethereum node, which is necessary to interact with the Ethereum blockchain. 


> **Note**  
>Replace 'https://example.com/ethereum/rpc' with the actual URL of your Ethereum provider, such as Infura.

### Define Contract Address and ABI
```
const contractAddress = 'your_contract_address';
const contractABI = [...]; // Replace with the ABI of your smart contract
```
- Specify the Blockchain network address of the smart contract you want to interact with
- Provide the Contract API with functions and parameters

> **Note**  
>Replace 'your_contract_address' with the actual address of your smart contract

### Create the Contract Instance
```
const contract = new ethers.Contract(contractAddress, contractABI, provider);
```
- This represents your smart contract by creating an instance of the ethers.Contract class.
- Use previously created address, ABI, and provider as arguments

### Define Two Example Functions 
These functions call the smart contract functions.
```
async function getSupportedSymbols() {
  try {
    const supportedSymbols = await contract.getSupportedSymbols();
    console.log('Supported Symbols:', supportedSymbols);
  } catch (error) {
    console.error('Error calling getSupportedSymbols:', error);
  }
}

// Example: Call the getCurrentPriceWithDecimals function
async function getCurrentPriceWithDecimals(symbol) {
  try {
    const { _price, _timestamp, _assetPriceUsdDecimals } =
      await contract.getCurrentPriceWithDecimals(symbol);
    console.log('Price:', _price);
    console.log('Timestamp:', _timestamp);
    console.log('Price Decimals:', _assetPriceUsdDecimals);
  } catch (error) {
    console.error('Error calling getCurrentPriceWithDecimals:', error);
  }
}
```
- getSupportedSymbols(): Calls the getSupportedSymbols function of the smart contract.
- getCurrentPriceWithDecimals(symbol): Calls the getCurrentPriceWithDecimals function of the smart contract, passing a symbol as an argument.

### Calling Smart Contract Functions
```
getSupportedSymbols();
getCurrentPriceWithDecimals('BTC');
```
- Use previously defined functions to interact with smart contract functions.
- First calls *getSupportedSymbols* function to retrieve supported symbols and the calls *getCurrentPriceWithDecimals('BTC')* function to get the current price of BTC

<details>
<summary>Complete Code for Calling Two Functions</summary>

```
const ethers = require('ethers');

// Replace 'your_rpc_url' with your Ethereum provider's URL (e.g., Infura)
//const provider = new ethers.JsonRpcProvider('your_rpc_url');
const { JsonRpcProvider } = require('ethers');
const rpcUrl = 'https://example.com/ethereum/rpc';

const provider = new JsonRpcProvider(rpcUrl);


// Replace 'contractAddress' with the address of the smart contract that implements the interface
const contractAddress = 'your_contract_address';

// Replace 'ABI' with the ABI of the smart contract
const contractABI = [
  // Function 1: getSupportedSymbols
  {
    constant: true,
    inputs: [],
    name: 'getSupportedSymbols',
    outputs: [{ name: '_supportedSymbols', type: 'string[]' }],
    type: 'function',
  },
  // Function 2: getCurrentPriceWithDecimals
  {
    constant: true,
    inputs: [{ name: '_symbol', type: 'string' }],
    name: 'getCurrentPriceWithDecimals',
    outputs: [
      { name: '_price', type: 'uint256' },
      { name: '_timestamp', type: 'uint256' },
      { name: '_assetPriceUsdDecimals', type: 'uint256' },
    ],
    type: 'function',
  },
];

// Create an ethers.js contract instance
const contract = new ethers.Contract(contractAddress, contractABI, provider);

// Example: Call the getSupportedSymbols function


// Example usage:
getSupportedSymbols();
getCurrentPriceWithDecimals('BTC');

```
</details>
<br>

## Run the JavaScript Code

### Step 1: Setup the Development Environment
Make sure you have installed the Node.js environment. Download and install Node.js from the website ['https://nodejs.org/'](https://nodejs.org/).

### Step 2: Create a New Project Directory
Create a new directory and navigate to that directory.
```
mkdir ethereum-contract-interaction
cd ethereum-contract-interaction
```
### Step 3: Create a JavaScript File
Create a JavaScript file (e.g., contract-interaction.js) in your project directory and add the above code to the file.

### Step 4: Configure Blockchain Network RPC URL and Contract Address
Make sure you have replaced below parameters with actual values.
- <BLOCKCHAIN_NETWORK_URL> - Replace with the URL of your Blockchain provider 
- <YOUR_CONTRACT_ADDRESS> - Replace with the Node address of the smart contract you want to interact with
- ContractABI -Replace contractABI with the ABI of your specific smart contract. Make sure it matches the functions and data structures of your contract.

### Step 5: Initialize the Node.js Project
Run the following command inside the project folder.
```
npm init -y
```
This command generates the *package.json* file to track project metadata and dependencies.

### Step 6: Install Ethers.js Package
Run the following command to install the ethers.js library to the project.
```
npm install --save ethers
```
This command adds the dependency code to the package.json file.

### Step 7: Run the JavaScript File
Run the following command to execute the requiredJavaScript file.
```
node contract-interaction.js
```
This command will execute the JavaScript code by connecting to the Blockchain network, creating the contract instance, and calling specified functions.

### Step 8: Verify the Output
If everything configured correctly and code executed without any error, the two functions *getSupportedSymbols()* and *getCurrentPriceWithDecimals('BTC')* should print the results to the console.

Sample output can be as below. The actual symbols and values will depend on the implementation of the smart contract and the symbol you provide to the function.
- getSupportedSymbols() output:
```
Supported Symbols: ['ETH', 'BTC', 'LINK', ...]
```

- getCurrentPriceWithDecimals(symbol) output:
```
Price: 45000
Timestamp: 1633442196
Price Decimals: 2
```



