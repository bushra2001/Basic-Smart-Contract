# Writing first Hello World Contract in Solidity

## Setting up the environment 

1. Install and set up our metamask account. 
2. Create an alchemy app.

### Creating alchemy app:

Sign up for your free account and get to create an app. 

- Environment - Staging
- Chain - Ethereum
- Network - Rinkeby

![alt text](https://lh6.googleusercontent.com/Bb5Mjaz4jGyF-_e9RHFtSRnSO_0nZTEgN9IuMjhkFCGL0vTfnpTdAzqXnNTo2qktp0uiR3gKmcokgX1bssf0sF9p-J5PmJU6HL7srmTClorF_hQVvjNtKcBGb_1zQw2Pd_ihqW_N)

API key and HTTP address is important, we will use it in our project later.
![alt_text](https://lh3.googleusercontent.com/GCh8lNY9s3lIBMPUX9-HdalprHLxldLq5KDzrq_9UmZXR1wixjsFIYv6JaBmFGN9pCY0vI4FrS8dLs_1HoxfHN2EUVrxCmkTGzI1_QCWH8gw-an-uCG9MU4WilBiJGzPKa54TTA3)

### Creating  MetaMask wallet 

Here are the installation steps:

- Go to MetaMask.io
- Click Download and Install the Chrome Extension.
- Setup your secure password. 
-  The next step is the most important one.
- Secure your 12-word phrase properly, never share it with anyone. Write it somewhere because if you lose it, you will never have a way to recover your account. So be mindful of that.
Account is created and you must have received a public address. The public address will be in the pattern of:

Example: 0x*********************************

It is completely safe to share this address publicly to accept, buy, trade or store Ethereum based crypto.

### Changing your network on MetaMask
We will switch to Rinkeby Network, which is a test network that pretty much is a simulation of Ethereum blockchain production. Just open chrome and switch your network to Rinkeby, if you are not able to see it. 

Here are the steps to turn on test networks

- Go to settings
- Open Advanced
- Scroll down to Show Test Networks
- Turn on
![alt_text](https://lh3.googleusercontent.com/J1aA9vZcf8gE3h9ypNI2nQ0-wRypnCCCwNBDHtc7C9qcyzlkbOmlb6IDUxxN1xIwQpfIwSPZrmXy-C5hS65lcFIKg5U0LZaXhGw_y2QxGurmhwZSHcJwK0gk5KCaUpu45pmz8jl2)

### Get some fake ETH:
Try the following websites and try to get some fake ETHs. This fake money will be used for deploying your contract and doing transactions on your contract. This is not real money, you can’t buy NFTs, or other assets via these ETH.

All you have to do is to drop your public address on the following links and the ETH will be transferred.

- https://faucets.chain.link/rinkeby
- https://rinkeby-faucet.com/

### Get your private MetaMask key:
Open the metamask extension to find your private key. Donot share your private key with anyone.
![alt_text](https://metaschool.s3-ap-southeast-1.amazonaws.com/images/Hrpx2AwPanh5OLiGRAV8U3AMBi8NMecZPCYuG8g5.png)

## Writing the Solidity Contract:

- Install [Nodejs](https://nodejs.org/en/)
- Install [VScode](https://code.visualstudio.com/)

Open terminal and run following commands.
```
 mkdir Hello-World
 
 cd Hello-World
 
 ls
 
 npm init --yes
 
 npm install --save-dev hardhat
 
 npx hardhat
```

When you run the last command, you will get an option to create an Empty project with hardhat config. 
copy the code
Now let's open in project in VScode. Open the Hardhat config file.
Install Solidity Extension in VScode to help with syntax and coding 
Creating Directories for Code
Now we will create two directories, contracts, scripts.

The contracts directory will have all the contracts for the project and scripts directory will have all the deployments scripts and other stuff related to the project. By now the structure of your project will look something like this.
```
HelloWorld

> contracts

> node_modules

> scripts

hardhat.config.js

package-lock.json

Package.json
```
The contracts directory will have the contract of your Hello World. Create a HelloWorld.sol file in the contracts folder and write the following code. 


 
 ```
    contract HelloWorld {
    
    //events
    //states
    //functions
 
    event messagechanged(string oldmsg, string newmsg);
 
    string public message;
 
    constructor(string memory firstmessage) {
        message = firstmessage;   
    }
 
    function update(string memory newmesssage) public {
        string memory oldmsg = message;
        message = newmesssage;
 
        emit messagechanged(oldmsg, newmesssage);
 
    }}
   ``` 


We start with mentioning the version of the solidity that we are using and then write the actual contract. A smart contract has states, functions and events. 

- The states are usually variables, tokens, NFTs whose state we want to maintain in the contract.
- In order to read, write or change the states, we use functions.  
- Events are triggers that are activated based on a transformation in a state, a call to a function etc. So our code right now has a state variable called ‘message’, a function called ‘update’ and and event called ‘messagechanged’.
- This is a basic HelloWorld code that takes a string when the smart contract is first time executed and if we want we can change that value to a new message as well.

Now that we have written the contract, the next step is to prepare for the deployment. 

## Deployment:

Run following commands in terminal;
```
npm install dotenv --save

touch .gitignore
```
Now go ahead and create .env file at the base of your project. Open your .gitignore file and write .env there. 

All the secrets and important keys related to your project will be stored in .env file and we can access this data whenever and wherever. In the gitignore file we simply write .env, it tells git to ignore that file from future commits. 

Open the .env file you have just created. Add your MetaMask Private Key and Alchemy App HTTP URL there. Should be something like this. 

```
PRIVATE_KEY=YOUR-PRIVATE-KEY

API_URL_KEY=YOUR-ALCHEMY-APP-URL

API_KEY=YOUR-ALCHEMY-APP-KEY
```
We will update our hardhat config file to setup Rinkeby Deployment.

```
require('dotenv').config(); //all the key value pairs are being made available due to this lib

require('@nomiclabs/hardhat-ethers');
 
const {API_URL_KEY, PRIVATE_KEY} = process.env; //environment variables are being loaded here.
 
module.exports = {
  solidity: "0.7.3",
  defaultNetwork: 'rinkeby',
  networks: {
    hardhat: {},
    rinkeby: {
        url: API_URL_KEY,
        accounts: [`0x${PRIVATE_KEY}`]
    }
  }
};
```
### Writing Deployment Script:

Now is the time to write the deployment script. Now, we will create a deploy.js file in the scripts folder and this file will contain all the logic for deployment. Before that we run the following command in the terminal. 
```
npm install --save-dev @nomiclabs/hardhat-ethers
```
deploy.js file;
```
const { ethers } = require("hardhat");
async function main() {
 
   const HelloWorld = await ethers.getContractFactory('HelloWorld');
 
   const hw = await HelloWorld.deploy("Hello World! Bingo");
 
   console.log('Contract Deployed to:', hw.address);
}
 
main().then(() => process.exit(0))
.catch(error => {
 console.error(error);
 process.exit(1);
});
```
 
Run the following command in terminal.
```
npx hardhat run scripts/deploy.js --network rinkeby
```
If all goes well, your contract will be deployed and you will be able to see the address of the contract on the terminal. Copy that and save in your .env file, we will use it later to interact with the contract.  

### Interacting with the Deployed Contract.

In the same scripts folder, create a new file interact.js. And add the following code.
```
const { ethers } = require("hardhat");
 
const API_KEY = process.env.API_KEY; //get from alchemy
const CONTRACT_ADDRESS = process.env.CONTRACT; //deployed contract address
const PRIVATE_KEY = process.env.PRIVATE_KEY; //metamask
 
const contract = require('../artifacts/contracts/HelloWorld.sol/HelloWorld.json');
 
// provider - Alchemy
const alchemyProvider = new ethers.providers.AlchemyProvider(network="rinkeby", API_KEY);
 
// signer - you
const signer = new ethers.Wallet(PRIVATE_KEY, alchemyProvider);
 
// contract instance
const helloWorldContract = new ethers.Contract(CONTRACT_ADDRESS, contract.abi, signer);
 
async function main() {
 
    const message = await helloWorldContract.message();
    console.log("the message is "+ message);
 
    const tx = await helloWorldContract.update("Good Bye, World!");
    await tx.wait();
 
    const nmessage = await helloWorldContract.message();
    console.log("the new message is "+ nmessage);
}
 
main()
.then(() => process.exit(0))
.catch(error => {
  console.error(error);
  process.exit(1);
});
```
Ether.js library gives us providers, which are basically the interface for our interaction with the Ethereum Blockchain nodes. When a request is made, it is sent to multiple backends simultaneously. As responses from each backend are returned, they are checked that they agree. Once a quorum has been reached (i.e. enough of the backends agree), the response is provided to your application. 

Signers is an abstraction of an ethereum account. The signers can be used to sign messages and transactions which can result in calling function, changing state variables etc. Here we are sharing our account private key, because we are the signers of this transaction. 

Rest of the code is very much the same, we fetch the current value of the message and then replace it with the new one. Run the following command again but this time, we will call the interact.js file.
```
npx hardhat run scripts/interact.js --network rinkeby
```
You will see something like this in terminal.
```
the message is Hello World! Bingo
the new message is Good Bye, World!
```
***********END***********
