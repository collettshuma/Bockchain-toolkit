# Bockchain-toolkit

Table of Contents
Set up a personal Blockchain
Develop smart contracts
Test smart contracts
Connect to a public blockchain
Deploy Smart Contracts
Run scripts
Connect to the blockchain with your web browser
Write a JavaScript application that talks to the blockchain
Personal Blockchain
The first item in the blockchain developer's toolkit is a personal blockchain, which is a local development blockchain that can be used to mimic the behavior of a public blockchain. I recommend using Ganache as your personal blockchain for Ethereum development. It will allow you to deploy smart contracts, develop applications, and run tests. It is available on Windows, Mac, and Linux as as a desktop application and a command line tool!

Ganache Personal Blockchain Application
I'll walk you through setting up the desktop application in this tutorial. You can find the latest release for your operating system here. Once you've downloaded the archived package, extract the installer and run through the setup steps. Once you've installed it, you should see a this screen whenever you open it:

Ganache Personal Blockchain Application
Yay! 🎉 Now you have a personal blockchain network running! You can see some details about the server Ganache is running on, along with a list of accounts connected to the network. Each account has been credited with 100 ether. This is a huge time saver! If you were to you create your own personal blockchain network from scratch, or develop your application on a test network, you would have to create all 10 accounts manually and credit each account with ether. Thankfully Ganache has already done this for us so that we don't have to worry about it.

There are four different pages available in the Ganache interface:

The Accounts Page - this shows you all of the accounts that are automatically generated, along with their balances.
The Blocks Page - this shows you each block that has been mined on the personal blockchain network, along with the gas cost and transactions.
The Transactions Page - this lists all the transactions that have taken place on the personal blockchain.
The Logs Page - this shows you all the server logs that you might need when debugging your application.
Also notice the is a search bar at the top, which allows you to search for any block or transaction on the personal blockchain network!

You can customize some of Ganache's features by visiting the Settings page, which you can access by clicking the gear icon at the top right corner of the user interface. Here are some settings you might be interested in:

Ganache Personal Blockchain Application
The Server Page - this manages the details about the network connection, like the network id, port, hostname, and auto-mining status.
The Accounts & Keys Page - this tracks the number of accounts that are generated automatically, as well as the amount of ether each account credited with. It also allows you to set a custom mnemonic seed phrase for generating accounts. This is useful if you want to import accounts from another wallet service like Metamask (more on this later).
The Chain Page - this allows you to set the gas limit and gas price for the network.
The Advanced Page - this gives you logging options, like the ability to save log files, and configure verbose output. You can also opt in/opt out of application analytics reporting here.
Note that you must click Restart inside Ganache to apply the new settings after you have changed them.

Develop Smart Contracts
Now that you have a private blockchain running, you need to configure your environment for developing smart contracts. The first dependency you'll need is Node Package Manager, or NPM, which comes with Node.js. You can see if you have node already installed by going to your terminal and typing:

$ node -v
If you don't have node already installed you can visit the Node.js websiteto download it.

Now let's install the Truffle Framework, which provides a suite of tools for developing Ethereum smart contacts with the Solidity programming language.

Truffle Blockchain Smart Contract Development Framework
Here is an overview of all the functionality we'll get with the Truffle Framework:

Smart Contract Management - write smart contracts with the Solidity programming language and compile them down to bytecode that be run on the Ethereum Virtal Machine (EVM).
Automated Testing - write tests against your smart contracts to ensure that they behave the way you want them to. These tests can be written in JavaScript or Solidity, and can be run against any network configured by Truffle, including public blockchain networks.
Deployment & Migrations - write scripts to migrate and deploy smart contracts to any public Ethereum blockchain network.
Network Management - connect to any public Ethereum blockchain network, as well as any personal blockchain network you might use for development purposes.
Development Console - interact with smart contracts inside a JavaScript runtime environment with the Truffle Console. You can connect to any blockchain network that you've specified within your network configuration to do this.
Script Runner - write custom scripts that can run against a public blockchain network with JavaScript. You can write any arbitrary code inside this file and run it within your project.
Client Side Development - configure your truffle project to host client side applications that talk to your smart contracts deployed to the blockchain.
You can install Truffle with NPM in your command line like this:

$ npm install -g truffle
Now that truffle is installed, let's create a new project like this:

$ mkdir blockchain-toolkit
$ cd blockchain-toolkit

Now let's initialize a new Truffle project inside the newly created directory:

$ truffle init
Now let's create a package.json file to install some project dependencies that will be invaluable for our blockchain developer toolkit. You can do that from the command line like this:

$ touch package.json
You can bootstrap all of the dependencies for your project by simply copy-and-pasting the code below into your package.json file:

{
  "name": "blockchain-toolkit",
  "version": "1.0.0",
  "description": "The Complete Blockchain Developer Toolkit for 2019 & Beyond",
  "main": "truffle-config.js",
  "directories": {
    "test": "test"
  },
  "scripts": {
    "dev": "lite-server",
    "test": "echo \"Error: no test specified\" && sexit 1"
  },
  "author": "gregory@dappuniversity.com",
  "license": "ISC",
  "devDependencies": {
    "bootstrap": "4.1.3",
    "chai": "^4.1.2",
    "chai-as-promised": "^7.1.1",
    "chai-bignumber": "^2.0.2",
    "dotenv": "^4.0.0",
    "ganache-cli": "^6.1.8",
    "lite-server": "^2.3.0",
    "nodemon": "^1.17.3",
    "solidity-coverage": "^0.4.15",
    "truffle": "5.0.0-beta.0",
    "truffle-contract": "3.0.6",
    "truffle-hdwallet-provider": "^1.0.0-web3one.0"
  }
}
Now you can install the dependencies from the command line like this:

$ npm install
Now that the dependencies are installed, let's examine the project directory structure that we just created:

Truffle Project Directory Structure
contracts directory: this is where all smart contacts live. We already have a Migration contract that handles our migrations to the blockchain.
migrations directory: this is where all of the migration files live. These migrations are similar to other web development frameworks that require migrations to change the state of a database. Whenever we deploy smart contracts to the blockchain, we are updating the blockchain's state, and therefore need a migration.
node_modules directory: this is the home of all of our Node dependencies we just installed.
test directory: this is where we'll write our tests for our smart contract.
truffle-config.js file: this is the main configuration file for our Truffle project, where we'll handle things like network configuration.
Now let's start developing a smart contract by creating a new file in the contracts directory like this:

$ touch ./contracts/MyContract.sol
Inside here, let's develop our simple smart contract. It will look like this:

pragma solidity ^0.4.24;

contract MyContract {
    string value;

    constructor() public {
        value = "myValue";
    }

    function get() public view returns(string) {
        return value;
    }

    function set(string _value) public {
        value = _value;
    }
}
This is a basic Solidity smart contract that can run on the Ethereum blockchain. It is a simple storage contract that can be accessed by anyone connected to the network. We'll keep this example simple so that we can focus on the tools highlighted in this tutorial. Let me explain this code further:

pragma solidity ^0.4.24; - this line declares the version of the solidity programming language we're using.
string value; - this declares a state variable called value. This will give us a way to store a string value to the blockchain inside the smart contract.
contract MyContract { ... } - this is how we declare the name of the smart contract. All of the code that belongs to the smart contract is contained inside the curly braces.
constructor() public { ... } - this is the contract's constructor function which is called whenever the contract is deployed to the network. This function has the public function modifier to ensure that it is available to the public interface. Inside this function, we set the value of the public variable value to "myValue".
function get() ... - this function allows us to read the value of the value state variable. Its visibility is set to public so that external accounts can access it. It's also contains the view modifier and specifies a string return value.
function set() ... - this function allows us to set the value of the value state variable, by accepting an argument for its new value. Its visibility is set to public so that external accounts can access it.
Now let's compile the smart contract and ensure that there are no errors:

$ truffle compile
Yay! 🎉 You've just written your first smart contract with this complete blockchain developer toolkit. You should notice that a new file was generated whenever you compiled the smart contract at the following path: `./build/contracts/MyContract.json`. This file is the smart contract ABI file, which stands for "Abstract Binary Interface". This file has many responsibilities, but two that I will highlight here:

It contains the compiled bytecode version of the Solidity smart contract code that can be run on a the Ethereum Virtual Machine (EVM), i.e., an Ethereum Node.
It contains a JSON representation of the smart contract functions that can be exposed to external clients, like client-side JavaScript applications.
We will use both of these functionalities later in this tutorial.

Now let's look at another powerful tool in our blockchain developer toolkit: the Truffle console. This is a command line tool that will allow us to interact with the smart contract in a JavaScript runtime environment. It is very useful for developing smart contracts. However, we cannot run the Truffle console because our application is not yet connected to the Ganache personal blockchain network we set up in the first section. To talk to the smart contract on the personal blockchain network inside the Truffle console, we must do a few things:

Update our project's configuration file to specify the personal blockchain network we want to connect to (Ganache).
Create a migration script that tells Truffle how to deploy the smart contract to the personal blockchain network.
Run the newly created migration script, deploying the smart contract to the personal blockchain network.
First, we'll update the project configuration file to specify the personal blockchain network we want set up in the first section. Find the file truffle-config.js and paste the following code:

module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",
      port: 7545,
      network_id: "*" // Match any network id
    }
  },
  solc: {
    optimizer: {
      enabled: true,
      runs: 200
    }
  }
}
Note: these should match the default settings provided by the Ganache personal blockchain network. If you changed any settings inside the Ganache settings page, like the port, those should be reflected here.

Next, we'll create a migration script inside the migrations directory to deploy the smart contract to the personal blockchain network. From your project root, create a new file from the command line like this:

$ touch migrations/2_deploy_contracts.js
Notice that we number all of our files inside the migrations directory with numbers so that Truffle knows which order to execute them in. Inside this newly created file, you can use this code to deploy the smart contract:

var MyContract = artifacts.require("./MyContract.sol");

module.exports = function(deployer) {
  deployer.deploy(MyContract);
};
First, we require the contract we've created, and assign it to a variable called "MyContract". Next, we add it to the manifest of deployed contracts to ensure that it gets deployed when we run the migrations. Now let's run this migration script from the command line like this:

$ truffle migrate
Now that we have successfully migrated the smart contract to the personal blockchain network, let's open the console to interact with the smart contract. You can open the truffle console from the command line like this:

$ truffle console
Now that we're inside the console, let's get an instance of our deployed smart contract and see if we can read the value from the contract. From the console, run this code:

MyContract.deployed().then((instance) => { app = instance } )
Here MyContract is the name of the variable that we created in the migration file. We retrieved a deployed instance of the contract with the deployed() function, and assigned it to an app variable inside the promise's callback function.

Now we can read the storage value that was set by the smart contract when it was deployed to the personal blockchain network:

app.get()
// => 'myValue'

Now we can set a new value like this:

app.set('New Value')

We can read that the value was updated like this:

app.get()
// => 'New Value'

Yay! 🎉 You've just learned how to use the Truffle console, and added a new tool to your blockchain developer toolkit! You can exit the Truffle console by typing this command:

.exit
Test Smart Contracts
The next invaluable tool in the blockchain developer toolkit is the Truffle test runner. Testing smart contracts is a vital part of the blockchain development lifecycle for a few reasons:

1. All of the code on the Ethereum blockchain is immutable; it cannot change. If the contract contains any bugs, we must disable it and deploy a new copy. This new copy will not have the same state as the old contract, and it will have a different address.

2. Deploying contracts costs gas because it creates a transaction and writes data to the blockchain. This costs ether, and we want to minimize the amount of ether we ever have to pay.

3. If any of our contract functions that write to the blockchain contain bugs, the account who is calling this function could potentially waste ether, and it might not behave the way they expect.

Now let's write some tests. Make sure you have Ganache running first. Then, create a new test file in the command line from the root of your project like this:

$ touch test/MyContract.js
We'll write all our tests in JavaScript inside this file with the Mocha testing framework and the Chai assertion library. These come bundled with the Truffle framework, and are invaluable tools in the blockchain developer toolkit. We'll write all these tests in JavaScript to simulate client-side interaction with our smart contract, much like we did in the console. We'll also use a lot of nice new features of ES6 like arrow functions and async/await. Here is all the code for the tests:

const MyContract = artifacts.require('./MyContract.sol');

contract('MyContract', (accounts) => {
  it('initializes with the correct value', async () => {
    const myContract = await MyContract.deployed()
    const value = await myContract.get()
    assert.equal(value, 'myValue')
  })

  it('can update the value', async () => {
    const myContract = await MyContract.deployed()
    myContract.set('New Value');
    const value = await myContract.get()
    assert.equal(value, 'New Value')
  })
})

Let me explain this code. First, we require the require the contract and assign it to a variable, like we did in the migration file. Next, we call the "contract" function, and write all our tests within the callback function. This callback function provides an "accounts" variable that represents all the accounts on our blockchain, provided by the Ganache private blockchain network.

The first test checks that the contract was initialized with the value by calling the get() function and checking its return value. I have used the ES6 async/await pattern to retrieve this value, which is an invaluable strategy for resolving asynchronous calls to smart contracts in JavaScript. This is an alternative to other strategies like promises and callback functions.

The next test ensures that we can set the storage value by first calling the set() function, and then the get() function to ensure that the value was updated.

Now let's run the tests from the command line like this:

$ truffle test
Yay, they pass! 🎉 Now you've added a new tool to your blockchain developer toolkit!

Connect to Public Blockchain
Now I'll show you how to connect your Truffle project to a public blockchain network. Up until this point, we've used a personal blockchain (Ganache) that is only accessible by us on our local development machines. Now we want to connect to a public Ethereum network. The eventual goal is to deploy our project to the Mainnet, this is the "real" Ethereum network where the Ethereum cryptocurrency, or ether, has real value. For now, we will connect our project to a test network.

Here are a few reasons why we want to use a test network:

We want to see how our smart contracts behave on a public blockchain. While the Ganache personal blockchain is great for local development, it does not behave exactly like a public blockchain.
It will allow us to test our project on a public blockchain network without the liability of losing funds or compromising security on the Ethereum Main net.
Ethereum has several test networks. For now, we will use the Kovan test network.

In order to connect our project to a public blockchain, we need to do a few things:

Obtain a wallet to manage our account on the network
Connect to an Ethereum node
Update our project settings to access the Ethereum node
First, we'll obtain a wallet to manage our account on the public blockchain network. To make things easy, let's use the wallet provided by Ganache when we started our personal blockchain network. Because of how blockchains work, this wallet is valid on a public blockchain as well as our personal blockchain! Open up Ganache, and view the accounts page, which is the default page. You should see a section called "Menmonic". It looks like this:

Ganache Personal Blockchain
This is a seed phrase that is used to build the wallet that is managed by Ganache. We can use this seed phrase to cryptographically rebuild our own wallet in order to connect to the public Ethereum blockchain network. Go ahead and copy this value.

Now let's create a secret place to store this value. Remember, this is a secret value that you should not store with anyone! Create a .env file in the root of your project like this:

$ touch .env
We'll use this file to store environment variables, or secrets for our project. We'll read the values from this file inside our project's configuration file in the next few steps. Go ahead and store your mnemonic seed phrase in this file like this:

MNEMONIC="your mnemonic seed phrase goes here"
Now that we've created our wallet, we need access to an Ethereum node in order to connect to the public blockchain network. There are a few ways you could do this. For one, you could run your own Ethereum node with Geth or Parity. But this requires you to download a lot of data from the blockchain and keep it in sync. This is a huge headache if you've ever tried to do this before.

Mostly for convenience, you can use Infura to access an Ethereum node without having to run one yourself. Infura is a service that provides a remote Ethereum node for free. All you need to do is sign up and obtain an API key and the RPC URL for the network you want to connect to.

Infura Ethereum Node Service
Once you've signed up, your Infura RPC URL should look like this:

https://kovan.infura.io/YOUR_INFURA_API_KEY
Now we can keep track of the infura api key inside the .env file like this:

INFURA_API_KEY=YOUR_INFRA_API_KEY
MNEMONIC="your mnemonic seed phrase goes here"
Now it's time to update our project's network configuration settings with our wallet seed phrase and our Infra RPC URL in order to connect to the public blockchain network. Let's update the truffle-config.js file to look like this:

require('dotenv').config();
const HDWalletProvider = require('truffle-hdwallet-provider');

module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",
      port: 7545,
      network_id: "*" // Match any network id
    },
    kovan: {
      provider: function() {
        return new HDWalletProvider(
          process.env.MNEMONIC,
          `https://kovan.infura.io/${process.env.INFURA_API_KEY}`
        )
      },
      gas: 5000000,
      gasPrice: 25000000000,
      network_id: 42
    }
  },
  solc: {
    optimizer: {
      enabled: true,
      runs: 200
    }
  }
}

If you look at the code, the first line allows us to read the settings from the .env file we created with the dotenv library. Then we're able to create a new wallet from our seed phrase with truffle-hd-wallet-provider. Then, we add the configuration for the kovan test network to our list of networks in our project.

Now let's connect to the public blockchain network attaching the Truffle console to the public test network. We can do that like this:

$ truffle console --network kovan
Now, let's read some data from the blockchain to verify our connection. Let's get some information about the latest block. Type this code into your console:

web3.eth.getBlock('latest').then(console.log)
You should see output that looks something like this:

{ author: '0x00d6cc1ba9cf89bd2e58009741f4f7325badc0ed',
difficulty: '340282366920938463463374607431768211454',
extraData: '0xde830201088f5061726974792d457468657265756d86312e33302e30827769',
gasLimit: 8000000,
gasUsed: 122548,
hash: '0x196ffc30728456c270be1ff835802a78fb274e2db8774bb948ffe7d5e2dba1e3',
logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
miner: '0x00D6Cc1BA9cf89BD2e58009741f4F7325BAdc0ED',
number: 9592894,
parentHash: '0x7facf90a01ee03598204cfd7e9b0230cc80d855d296c4f3f9ef5e63f7bce9bd2',
receiptsRoot: '0xd83e80c3f7947bd2b6d6b3afa05bcce3ffb7a12ce16dd9c20317aa0001a15173',
sealFields:
[ '0x841701fd92',
 '0xb841c10a581180badfcb14868f199483e79fe4bcd0ad38b7de5c0eb87cca8e44142f018f313869b6687cdaf2bfdf9f277bad4f9670b9a6d5cf8b6a49d8e74b4a7a0800' ],
sha3Uncles: '0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347',
signature: 'c10a581180badfcb14868f199483e79fe4bcd0ad38b7de5c0eb87cca8e44142f018f313869b6687cdaf2bfdf9f277bad4f9670b9a6d5cf8b6a49d8e74b4a7a0800',
size: 1185,
stateRoot: '0x992e4aaa4949a67edf7205c5f5fbccdaa1a57ec89d7c90fa6e2edf8cc7718851',
step: '386006418',
timestamp: 1544025672,
totalDifficulty: '3213849558151676063641678302953486816576181081',
transactions:
[ '0xf62eb685f91564c8a4ba97537fd4824d3b2c44eee7dcfbce67c18437c52326dd' ],
transactionsRoot: '0xf269832b7e4a4353952e697fa6427da30d94e33dc466a9a07c5f973116fd9857',
uncles: [] }
Hooray! 🎉 You've successfully connected your project to a public blockchain network! If you want to understand more about how blocks work, you can check out another article I have called Intro to Web3.js.

Deploy Smart Contracts
Now it's time to deploy the smart contract to the test network. We'll must complete a few steps in order to make this happen:

Obtain ether for the deployment
Deploy the smart contract
Verify the deployment
First, let's obtain some Ether for the deployment. Remember, creating a smart contract on the Ethereum blockchain costs "gas" in the form of ether. We have to pay money any time we make changes to the blockchain itself, and we're changing the blockchain whenever we deploy this smart contract. Thankfully, we're using a test network, so the gas that we pay is not worth any real money. In fact, we can obtain fake ether for the Kovan test network for free from a "faucet". We'll do that right now.

First you'll need the account you want to send ether to. Open Ganache and copy the address of the first account in the list. It should look something like this (note, use your real account address not this one):

0x498287d2B422813854bC27afCd13B1059FE13eD6
Now, visit this the Kovan faucet Gitter channel to obtain fake ether on the Kovan test network. Simply visit this chat room and paste in your account address. Your account should be funded shortly. You'll receive a confirmation in the chat room once your account has been funded. Maybe wait 5 minutes before you try to deploy the smart contract just to be safe.

Now that your account is funded, it's time to deploy the smart contract to the Kovan test network! You can do that from the command line like this:

truffle migrate --network kovan
You should see successful logging messages once the deployment has completed. Now open the truffle console to interact with the smart contract on the Kovan test network:

$ truffle console --network kovan
Now inside the console, do this:

truffle(kovan)> MyContract.deployed().then((c) => { contract = c })
Then:

truffle(kovan)> contract.get()
// => 'myValue'
Hooray! 🎉 You've successfully deployed the smart contract to a public test network! Feel free to play around with your smart contract in the console at this point.

Run Scripts
Truffle includes a script runner that can be used to execute custom scripts against any Ethereum network. This is very useful when performing routine tasks (have you ever tried to whitelist a bunch of addresses in an ICO, haha?). Let's create an example script from the root of our project like this:

$ touch script.js
Inside this newly created file, we can create a new script that will get information about the latest block from the Kovan test network, like we did previously in the console. Let's add this code to the script file:

module.exports = function(callback) {
  web3.eth.getBlock('latest').then(console.log)
}
Now we can run this script against the Kovan test network like this:

truffle exec script.js --network kovan
You should see an output log that looks something like this:

{ author: '0x007733a1fe69cf3f2cf989f81c7b4cac1693387a',
difficulty: '340282366920938463463374607431768211454',
extraData: '0xde830202018f5061726974792d457468657265756d86312e33302e31826c69',
gasLimit: 8000000,
gasUsed: 41104,
hash: '0x3f85540fad70740e2779d7330cd9ca969f3d842715ca57815856c142436adbe0',
logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
miner: '0x007733a1FE69CF3f2CF989F81C7b4cAc1693387A',
number: 9593107,
parentHash: '0x8c4b7838c5ecb7d0a0931c890d3cea3f62af7778f7037d70eb775f492a2ba57b',
receiptsRoot: '0xb9be3018b8575e8eb6a6942fba4ba1687d9a1290d2676cc9def409ece679a4f9',
sealFields:
[ '0x841701ff11',
 '0xb841c5c1dcefaae49dfbff3172d59cfb99c26f9f7894c2e2ef672ad1966735ea103235d58f3976f7aefafc8c5aaad36652d78606c094726c27feeba8ba7b7680bec900' ],
sha3Uncles: '0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347',
signature: 'c5c1dcefaae49dfbff3172d59cfb99c26f9f7894c2e2ef672ad1966735ea103235d58f3976f7aefafc8c5aaad36652d78606c094726c27feeba8ba7b7680bec900',
size: 1312,
stateRoot: '0x1880f43eb8b708cb7af54b8f1ca6d96926b84ba357bd147d26e97bd79f62fe04',
step: '386006801',
timestamp: 1544027204,
totalDifficulty: '3213922038295830223534396001744869783205220613',
transactions:
[ '0x02ed567352949e5b25b986f56544a8bf838496b79ad1b68bb1c2a85c4502a1a2' ],
transactionsRoot: '0xa45ce3cb13964f2ec1abff094aadb51997e438e3fdc72ee9f648c9b757df2c41',
uncles: [] }
Now let's replace the script with code that reads data from the smart contract we deployed to the Kovan test network. Replace the code in the script file with this:

const MyContract = artifacts.require("./MyContract.sol");

module.exports = async function(callback) {
  const contract = await MyContract.deployed()
  const value = await contract.get()
  console.log("Value:", value)
}
Again, we can run the script from the command line like this:

truffle exec script.js --network kovan
You should see the storage value from your smart contract logged to the console.

Awesome! Now you can leverage the power of the Truffle script runner in your blockchain developer toolkit.

Blockchain Enabled Web Browser
Now it's time to turn your web browser into a blockchain browser. Most major web browsers do not currently connect to blockchain networks, so we'll have to install a browser extension that allows them to do this.

Metamask Ethereum Wallet Browser Extension
I'll the Metamask extension for Google Chrome. To install Metamask, visit this link or search for the Metamask Chrome plugin in the Google Chrome web store. Once you’ve installed it, be sure that it is checked in your list of extensions. You’ll see the fox icon in the top right hand side of your Chrome browser when it’s installed. Reference the video walk through if you get stuck!

Once you've set up Metamask, it's time to import an account from Ganache so that we can connect to the blockchain. Go to the accounts page in the Ganache UI, and click the key symbol next to the first account in the list. This will expose the account's private key. Copy this to your clipboard, but not share this with anyone!

Metamask Ethereum Wallet Browser Extension
Now, we we want to import this account into Metamask. Open Metamask, click the multicolored icon in the top right hand corner, and click the "import account" option. Paste your private key here, and click "Import".

Metamask Ethereum Wallet Browser Extension
Hooray! You've just turned your web browser into a blockchain-powered web 3.0 browser! Feel free to reference the video at the beginning of the article if you get stuck.

Client Side App
Now let's create a client side application that talks to the smart contract on the blockchain. We'll create a simple app that does the following:

Shows the blockchain account we're connected with
Reads the storage value of the smart contract
Updates the storage value of the smart contract
The app will look like this:

Decentralized Ethereum Blockchain Smart Contract Application Dapp
We will need to set up several things in order to make this work, like:

Configure a web server to serve the client side application files
Import client side dependencies that will allow us to talk to the blockchain, and allow us to build the UI
Create the files for the client side application and write the code that runs the app
First, let's configure the web server. We'll use lite-server for this. To proceed, we must first install lite-server globally like this:

$ npm install -g lite-server
Now, we must add a configuration file that creates a base directory for all client-side files. This will take all of the smart contract ABI files that were created when we compiled our smart contracts and expose them to the root directory of the client side application. It will also expose the node_modules directory so that we can import dependencies. Let's create a new configuration file like this:

$ touch bs-config.js
Inside this file, paste the following code:

{
  "server": {
    "baseDir": [
      "./src",
      "./build/contracts"
    ],
    "routes": {
      "/vendor": "./node_modules"
    }
  }
}
Now, let's create a directory structure for the side application:

$ mkdir src
Inside this directory, we'll create two files, one for the HTML markup and one for the JavaScript code. We'll create the HTML markup file first:

$ touch ./src/index.html
Here is the HTML markup that will go inside this file:

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
    <title>Blockchain Developer Toolkit</title>

    <!-- Bootstrap -->
    <link href="vendor/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- https://getbootstrap.com/docs/4.1/examples/dashboard/ -->

    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <nav class="navbar navbar-dark fixed-top bg-dark flex-md-nowrap p-0 shadow">
      <a class="navbar-brand col-sm-3 col-md-2 mr-0" href="#">Blockchain Developer Toolkit</a>
      <ul class="navbar-nav px-3">
        <li class="nav-item text-nowrap">
          <small><a class="nav-link" href="#">Your Account: <span id="account"></span></a></small>
        </li>
      </ul>
    </nav>
    <div class="container-fluid">
      <div class="row">
        <main role="main" class="col-md-9 ml-sm-auto col-lg-10">
          <div class="d-flex justify-content-between flex-wrap flex-md-nowrap pt-3 pb-2 mb-3" style="margin-top: 40px;">
            <div id="loader" style="">
              <p class="text-center">Loading...</p>
            </div>
            <div id="content" class="col-lg-9" style="display: none;">
              <h2>My Contract</b></h2>
              <p>Here is the value stored on the blockchain: <span id="value"></span></p>

              <h5>Update the Value</h5>
              <form onSubmit="App.set(); return false;" class="" role="form">
                <div class="form-group">
                  <input id="newValue" class="form-control" type="text"></input>
                </div>
                <button type="submit" class="btn btn-primary">Set Value</button>
              </form>
            </div>
          </div>
        </main>
      </div>
    </div>

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="vendor/bootstrap/dist/js/bootstrap.min.js"></script>
    <script src="https://etherscan.io/jss/web3.min.js"></script>
    <script src="vendor/truffle-contract/dist/truffle-contract.js"></script>
    <script src="app.js"></script>
  </body>
</html>
I'll explain what's happening inside this file. First, I'll explain the dependencies.

Bootstrap - this is the client side framework that allows us to write nice looking UI without writing too much CSS or JS manually. I've imported the bootstap css file and js file inside the markup file.
Web3.js - this is the JavaScript library that connects our client side application to the blockchain. I've imported this file from the node_modules directory, masked as the vendor path that we configured inside the bs-config.js file. We'll use this library inside the app.js file. If you want to learn more about Web3.js, you can check out my other tutorial series here.
TruffleContract - this is the library that will create a JavaScript abstraction for the smart contract we developed in the previous section.
Now, I'll explain the markup. First, we have a simple header that displays the project name and the blockchain account we're connected with. Next, we have a content section that displays the current storage value of the smart contract. Then, we have a form that allows us to update the storage value. All of these elements get wired up inside the app.js file.

Now let's create a file for the JavaScript code:

$ touch ./src/app.js
Here is the JavaScript code that goes inside this file:

App = {
  web3Provider: null,
  contracts: {},
  account: '0x0',
  loading: false,
  contractInstance: null,

  init: async () => {
    await App.initWeb3()
    await App.initContracts()
    await App.render()
  },

  // https://medium.com/metamask/https-medium-com-metamask-breaking-change-injecting-web3-7722797916a8
  initWeb3: async () => {
    if (typeof web3 !== 'undefined') {
      App.web3Provider = web3.currentProvider
      web3 = new Web3(web3.currentProvider)
    } else {
      window.alert("Please connect to Metamask.")
    }
    // Modern dapp browsers...
    if (window.ethereum) {
      window.web3 = new Web3(ethereum)
      try {
        // Request account access if needed
        await ethereum.enable()
        // Acccounts now exposed
        web3.eth.sendTransaction({/* ... */})
      } catch (error) {
        // User denied account access...
      }
    }
    // Legacy dapp browsers...
    else if (window.web3) {
      App.web3Provider = web3.currentProvider
      window.web3 = new Web3(web3.currentProvider)
      // Acccounts always exposed
      web3.eth.sendTransaction({/* ... */})
    }
    // Non-dapp browsers...
    else {
      console.log('Non-Ethereum browser detected. You should consider trying MetaMask!')
    }
  },

  initContracts: async () => {
    const contract = await $.getJSON('MyContract.json')
    App.contracts.MyContract = TruffleContract(contract)
    App.contracts.MyContract.setProvider(App.web3Provider)
  },

  render: async () => {
    // Prevent double render
    if (App.loading) {
      return
    }

    // Update app loading state
    App.setLoading(true)

    // Set the current blockchain account
    App.account = web3.eth.accounts[0]
    $('#account').html(App.account)

    // Load smart contract
    const contract = await App.contracts.MyContract.deployed()
    App.contractInstance = contract

    const value = await App.contractInstance.get()
    $('#value').html(value)

    App.setLoading(false)
  },

  set: async () => {
    App.setLoading(true)

    const newValue = $('#newValue').val()

    await App.contractInstance.set(newValue)
    window.alert('Value updated! Refresh this page to see the new value (it might take a few seconds).')
  },

  setLoading: (boolean) => {
    App.loading = boolean
    const loader = $('#loader')
    const content = $('#content')
    if (boolean) {
      loader.show()
      content.hide()
    } else {
      loader.hide()
      content.show()
    }
  }
}

$(() => {
  $(window).load(() => {
    App.init()
  })
})
Let me explain this code. I'll point out each function and what it does.

First, the initWeb3() function adds the configuration needed to connect our web browser to the blockchain with Metamask. This is a copy-and-paste directly from Metamask's configuration specifications, as noted by the url in the code comment above the function.

Next, the initContracts() function uses the TruffleContract library to create a JavaScript abstraction of our smart contract that's deployed to the blockchain. We'll be able to use this abstraction to call our smart contract functions in this file.

The render() function lays out all of the content on the page, including the account we're connected with, and the current storage value of the smart contract.

The set() function allows us to update the storage value of the smart contract. We created an onSubmit() handler inside the markup file that triggers this whenever the form is submitted to update the storage value.

Now, let's start the server and view the client side app in the browser:

$ npm run dev
