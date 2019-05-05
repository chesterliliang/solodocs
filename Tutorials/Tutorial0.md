# Build your own ETH wallet app with **WOOKONG Solo**

You can get the whole code of this tutorial at [https://github.com/extropiescom/wookong-solo-tutorial-node](https://github.com/extropiescom/wookong-solo-tutorial-node)


## Requirements

### Skills

This tutorial will show you how to build your own cli (command line interface) ETH wallet application with **WOOKONG Solo** under cli step by step, at the beginning, you are assumed to be:

* Having basic knowledge about programming.
* Having basic knowledge about JavaScript programming and [Node.js](https://nodejs.org/)
* Having basic knowledge about blockchain.
* Having basic knowledge about [Ethereum and ETH](https://ethereum.org/). 
* Having basic knowledge about [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) and [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md)

Experience on [web3.js](https://github.com/ethereum/web3.js) may be helpful for reading this tutorial.

### Environments

**WOOKONG Solo** supports both Windows and macOS, so your development should based on:

* macOS Mavericks (10.9) and above

* Windows 7 SP1/8/8.1/10 x64 and above

Ensure you have to be on [Node.js](https://nodejs.org/) >= 10.x before you start with this tutorial.

You can use the following command to get your Node.js version:

```shell
node -v
```

## Goals

We are going to build a simple CLI ETH wallet with four basic commands as below, for parsing convenience, all parameters should be seprated with `-p`
1. info
   
   This command is used to get device info, and it does not need any other parameters.   

2. addr
   
   This command is used to get ETH address, and it needs only one parameter for derive path, address should be shown on device screen.
   
   **Example**  
   
   ```shell
   addr -p[0, 2147483692, 2147483708, 2147483648, 0, 0]
   ```

3. Get balance
   
   This command is used to get ETH balance on chain, and it needs only one parameter for derive path.
   
   **Example**  
   
   ```shell
   balance -p[0, 2147483692, 2147483708, 2147483648, 0, 0]
   ```

4. Send ETH to other addresses
   
   This command is used to transfer ETH, and it needs 3 parameters for derive path, recipient address and transfer value.
   
   **Example**  
   
   ```shell
   send -p[0, 2147483692, 2147483708, 2147483648, 0, 0] -p0x7F825230F5F2A26523999c98e0E3f7E2697085A9 -p0.0001
   ```


## Notice

This is a simple tutorial to show you the basic usage of **wookong-solo-lib**, although **WOOKONG Solo** is a financial level security hardware, we do not guarantee for any crypto currencies loss caused by improperly usage of **WOOKONG Solo** and **wookong-solo-lib**. Users should ensure the mnemonics are stored securely and check the transaction information shown on device screen carefully befor confirm it.

## Preparation


1. create a folder with name "wookong-solo-tutorial" use the following commands, you may change "wookong-solo-tutorial" to any name you like. 
   
   ```shell
   mkdir wookong-solo-tutorial
   cd wookong-solo-tutorial
   ```

2. `npm init`, then answer the questions to create package.json file, you may create it manually if you are familiar with it. You may also use the content below.
    ```json
    {
        "name": "wookong-solo-tutorial",
        "version": "1.0.0",
        "description": "A tutorial for showing how to use wookong-solo-lib",
        "main": "index.js",
        "scripts": {
            "test": "echo \"Error: no test specified\" && exit 1"
        },
        "author": "pengwei@extropies.com",
        "keywords": [
            "Ethereum",
            "WOOKONG",
            "tutorial"
        ],
        "license": "MIT",
    }
    ```

3. create a file named "index.js" with the following content, now we have a basic cli framework.
   
   ```js
    const readline = require('readline');

    const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
    prompt: 'WST> '
    });

    console.log('Welcome to WOOKONG Solo Tutorial Wallet(WST)!');
    console.log('USAGE:\ninfo\naddr derive_path\nbalance derive_path\nsend derive_path to value');
    console.log('Example:\nsend -p[0, 2147483692, 2147483708, 2147483648, 0, 0] -p0x7F825230F5F2A26523999c98e0E3f7E2697085A9 -p0.00001');
    rl.prompt();

    rl.on('line', async (line) => {
        const command = line.trim().split(' -p');
        try {
            switch (command[0]) {
                case 'info':
                    console.log('info command is not implemented now');
                    break;
                case 'addr':
                    console.log('addr command is not implemented now');
                    break;
                case 'balance':
                    console.log('balance command is not implemented now');
                    break;
                case 'send':
                    console.log('send command is not implemented now');
                    break;
                case 'exit':
                    console.log('Thank you for using WST wallet, bye!');
                    break;
                default:
                    console.log(`unknown command: '${command[0]}'`);
                    break;
            }
        } catch (error) {
            console.log('An error happened: ', error.message);
        }
        rl.prompt();
    }).on('close', () => {
        console.log('Thank you for using WST wallet, bye!');
        process.exit(0);
    });
   ```

4. run `node index.js` in command line, then you can see this little CLI frameworks, type `exit` to exit this program.