# Let's start

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
        "name": "wookong-solo-tutorial-node",
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
    console.log('USAGE:');
    console.log('info');
    console.log('init (generate|import)');
    console.log('foramt');
    console.log('addr <derive_path>');
    console.log('balance <derive_path>');
    console.log('nsend (<derive_path> <to> <value>)');
    console.log('Example');
    console.log('init import');
    console.log('send [0,2147483692,2147483708,2147483648,0,0] 0x7F825230F5F2A26523999c98e0E3f7E2697085A9 0.00001');
    rl.prompt();

    rl.on('line', async (line) => {
        const command = line.trim().split(' ');
        try {
            switch (command[0]) {
                case 'info':
                    console.log('info command is not implemented now');
                    break;
                case 'init':
                    console.log('init command is not implemented now');
                    break;
                case 'format':
                    console.log('format command is not implemented now');
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
