## Create Skeleton Project

             
    npx create-react-app dabit-tut
    cd dabit-tut
    npm install --save-dev hardhat
    npm install --save-dev @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai
    npx hardhat


Select 'create sample project', and y (default) on prompts.

## Update Configurations

1. Go to *hardhat.config.js*.

2. Update the module.exports section in *hardhat.config.js* with the following:

    -solidity version to 0.8.3
    -added paths
    -added networks

3. Rename the *sample-script.js* in the scripts folder to *deploy.js* since this script helps with the deployment.

// deploy.js uses *ethers.js* library to put our smart contract onto the ethereum blockchain by sending a message to the x0 address of ethereum blockchain with the data load being our compiled smart contract in bytecode.

## Compile and Deploy

    npx hardhat compile // to see things working
    npx hardhat node // start the Hardhat Network, which also gives us 20 Accounts from Account #0 to Account #19 for test use.

open another terminal

    npx hardhat run scripts/deploy.js --network localhost // this deploys to the local hardhat node/hardhat network


Note that the *deploy.js* script, by default, uses the *Account #0* as the sender of the transaction that creates the new contract on the blockchain. "Contract creation transactions are sent to a special destination address called the *zero address* (0x0)" - [Mastering Ethereum](https://github.com/ethereumbook/ethereumbook/blob/develop/06transactions.asciidoc#special-transaction-contract-creation). You can see this by comparing the *From: address* with the *Account #0* address.

## Connect Metamask

On MetaMask - select *localhost: 8545*
Import account using the private key from *Account #0* given to us.

We can send transaction from metamast to the contract? #TODO:

## To the Frontend - Startup React

    run npm start // starts up node server

Go to App.js and import:

    import { useState} from 'react';
    import { ethers } from 'ethers';
    import Greeter from './artifacts/contracts/Greeter.sol/Greeter.json' // imports the compiled ABI

## Code React Frontend
At 20 min of [Dabit Full Stack Guide](https://youtu.be/a0osIaAOFSE?t=1863)

See detailed notes in App.js. Below are high level steps that was taken to code it.

1. Set the usestate. #TODO:
2. Create 3 skeleton functions.
3. Code fetchGreeting.
4. Code 
5. Code 
...

## Deploy to Ropsten

#### Setup Metamask

1. Switch Metamask to Ropsten network. Create an Account if needed.
2. Get Ether at https://faucet.ropsten.be/ into your Metamask account.

#### Config Alchemy or Infura

1. Choose either [Alchemy](https://dashboard.alchemyapi.io/) or [Infura](https://infura.io/) as an Ethereum node that we will connect to.
2. On Alchemy "Create App" and select Ropsten as network and get the API Key.

#### Update *hardhat.config.js*

We now update our hardhat.config.js to add the Ropsten network. You will need the API endpoint from Alchemy. 

Also you will need to export the private key from the Ropsten account in your Metamask. This will be the account used to create/deploy the contract

1. Add the below to the networks section of hardhat.config.js

````

ropsten: {
   url: "<API url from Alchemy goes here.>",
   accounts: [`0x${process.env.PRIVATE_KEY`}] //this is a way to hide the private key. We put the private key in an environment file.
}
````

Put this in the environment file:

`export PRIVATE_KEY="<private key from metamask goes here>"`

//TODO: how to set environment variable

#### Deploy

`npx hardhat run script/deploy.js --network=ropsten`

We should see message giving us the deployed contract address.

#### Check Etherscan ropsten

1. Go to https://ropsten.etherscan.io/.
2. Copy the contract address, and paste into etherscan.

We should see the contract show up!

We should see that we spent a bit of Ether in Metamask as well.

# Create Token
at 38 min #TODO:
