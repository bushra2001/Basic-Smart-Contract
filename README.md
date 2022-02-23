# Writing first Hello World Contract in Solidity

## Setting up the environment 

1. Install and set up our metamask account. 
2. Create an alchemy app.

### Creating alchemy app:

Sign up for your free account and get to create an app. 

Environment - Staging
Chain - Ethereum
Network - Rinkeby

**photo**

API key and HTTP address is important, we will use it in our project later.

**photo**

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

### Get some fake ETH:
Try the following websites and try to get some fake ETHs. This fake money will be used for deploying your contract and doing transactions on your contract. This is not real money, you can’t buy NFTs, or other assets via these ETH.

All you have to do is to drop your public address on the following links and the ETH will be transferred.

- https://faucets.chain.link/rinkeby
- https://rinkeby-faucet.com/

### Get your private MetaMask key:
Open the metamask extension to find your private key. Donot share your private key with anyone.

## Writing the Solidity Contract:

- Install [Nodejs](https://nodejs.org/en/)
- Install [VScode](https://code.visualstudio.com/)

Open terminal and run following commands.

- mkdir Hello-World
- cd Hello-World
- ls
- npm init --yes
- npm install --save-dev hardhat
- npx hardhat

When you run the last command, you will get an option to create an Empty project with hardhat config. 
copy the code
Now let's open in project in VScode. Open the Hardhat config file.
Install Solidity Extension in VScode to help with syntax and coding 
Creating Directories for Code
Now we will create two directories, contracts, scripts.

The contracts directory will have all the contracts for the project and scripts directory will have all the deployments scripts and other stuff related to the project. By now the structure of your project will look something like this.

HelloWorld
> contracts
> node_modules
> scripts
hardhat.config.js
package-lock.json
Package.json

The contracts directory will have the contract of your Hello World. Create a HelloWorld.sol file in the contracts folder and write the following code. 
` 
pragma solidity >= 0.7.3;
 
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
 
    }
}
`
We start with mentioning the version of the solidity that we are using and then write the actual contract. A smart contract has states, functions and events. 

- The states are usually variables, tokens, NFTs whose state we want to maintain in the contract.
- In order to read, write or change the states, we use functions.  
- Events are triggers that are activated based on a transformation in a state, a call to a function etc. So our code right now has a state variable called ‘message’, a function called ‘update’ and and event called ‘messagechanged’.
- This is a basic HelloWorld code that takes a string when the smart contract is first time executed and if we want we can change that value to a new message as well.

Now that we have written the contract, the next step is to prepare for the deployment. 
