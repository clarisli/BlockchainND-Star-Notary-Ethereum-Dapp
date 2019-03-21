## Star Notary Dapp on Ethereum

In this project I created a ERC-721 token and deployed to Ethereum Rinkeby Test Network. This smart contract allows users to create a star with a token ID and look up a star with its token ID.

* **Truffle version**: v5.0.8
* **OpenZeppelin version**: v2.1.2
* **ERC-721 Token Name**: Star Token
* **ERC-721 Token Symbol**: ST
* **Token Address on the Rinkeby Network**: 0x4931115d8242888091638dAa865615a0B3eceb80


[image1]: ./misc/screenshot1.png
[image2]: ./misc/tests.png
[image3]: ./misc/stars.jpg

![alt text][image3]

## Setup

To setup the project, download the project and do the following:

### Install Truffle

* Use `truffle -v` to verify if you have Truffle installed.
* Use `npm install -g truffle` to install Truffle or update it to the latest version.

### Install and Configure Metamask

1. Install the extention [MetaMask](https://metamask.io/) for your browser to interact with dapps.
2. Create or restore your vault on Metamask
3. Create a file named `.secret` under the project directory.
4. Copy your secret mnemonic to `.secret`.

##### Configure the Private Network on Metamask:

1. Go to Metamask extention on your browser
2. Use option, Connect using “Custom RPC”, at address `http://127.0.0.1:9545/`
3. Use the Private Keys provided by Truffle to import at least two accounts.


### Run the Project

1. Run command `npm insall` under the project directory to install the project dependencies
2. Run command `truffle develop` to start the development console
3. Run command `compile` to compile the contract
4. Run command `truffle test` to run all the unit tests
5. Run command `migrate --reset` to migrate the contract to the local Ethereum network
6. Open another terminal window and run command `npm run dev` under the directory `./app`
7. Open the DAPP at [http://localhost:8080/](http://localhost:8080/)

### Deploy the Project on Rinkeby

#### Connect to Rinkeby with Infura

Use your own Infura project secret to connect to the public test network.

Infura allows you to connect to the Ethereum blockchain without running a full node. It's a lightweight alternative to downloading the entire blockchain to your local device. 

1. Create an account on [infura.io](https://infura.io/dashboard)
2. Create a project on Infura
3. Create a file named `.infura-secret` under the project directory.
4. Switch your porject's endpoint to Rinkeby then copy your project secret to `.infura-secret`.

#### Configure Rinkeby Network on Metamask

1. Go to Metamask extention on your browser
2. Use option, Connect using “Rinkeby Test Network”


## Smart Contract

I used `openzeppelin-solidity` library to implement the ERC721 token. The contract is at `/contracts/StarNotary.sol`.

* Set the name and symbol for my starNotary tokens at lines 14 to 15.
* Added a function `lookUptokenIdToStarInfo()` that looks up the stars using the Token ID, and then returns the name of the star. Find this at lines 56 to 59.
* Added a function called `exchangeStars()` in lines 62 to 68, so 2 users can exchange their star tokens. 
* Added a function called `transferStar()` that transfers a star from the address of the caller. In lines 71 to 74.

## Unit Tests
The unit tests are in `/test/TestStarNotary.js`, I added following four test cases:

* The token name and token symbol are added properly, lines 76 to 82.
* 2 users can exchange their stars, lines 84 to 95.
* Stars Tokens can be transferred from one address to another, lines 97 to 105.
* A user can look up for a star using its token id, lines 107 to 115.

![alt text][image2]

## Deploy to Rinkeby

I edited the `truffle-config.config` file to add settings to deploy the contract to the Rinkeby Public Network in lines 67 to 72. 


```
    rinkeby: {
      provider: () => new HDWalletProvider(mnemonic, `https://rinkeby.infura.io/${infuraKey}`),
      network_id: 4,
      gas: 4500000,
      gasPrice: 10000000000
    }
```

Then under the project directory I ran the command `truffle migrate --reset --network rinkeby` to deploy to Rinkeby.

The contract's address is `0x4931115d8242888091638dAa865615a0B3eceb80` and you can view it on [Etherscan](https://rinkeby.etherscan.io/address/0x4931115d8242888091638daa865615a0b3eceb80).

## Front End

![alt text][image1]

To allow users to look up for a star with its token ID, I added an async function `lookup()` in lines 42 to 47 of `./app/src/index.js` and a simple form in lines 41 to 53 of `./app/src/index.html` to call the function `tokenIdToStarInfo()` in the contract.

In addition, I also polished the UI with Bootstrap.

## Future Works

* Add more fields to the Star struct: right ascension, declination, centaurus, and magnitude.
* Update the front end to list all stars.
* Update the front end to allow users to buy or exchange a star.
* Update the front end to allow a user to view all stars that he/she owns.
* Update the front end to allow a user to sell a star.


    
