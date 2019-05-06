# Initialize your **WOOKONG Solo**

## `init` command

**Intergrate **wookong-solo-lib** into current project and get device info of connected **WOOKONG Solo****

There are 2 ways for you to initialize your **WOOKONG Solo**, one is generate seed randomly by **WOOKONG-Solo** itself, the other one is import mnemonics you have saved before. In this section, we will init a **WOOKONG Solo** to make it ready for ETH.


1. Before initializing **WOOKONG Solo**, we should ensure its lifecycle is [LIFECYCLE_AGREE](../../API/3-core.constants.md#clifecycle-definition), **WOOKONG Solo** with other lifecycles can not be initialized. Use [generateSeed(seedLen)](./4-Functions.md#generateseedseedlen) to generate seed randomly, [importSeed()](./4-Functions.md#importseed) to import mnemonics saved before. Add the following function to the end of `index.js`.
   
    ```js
    async function processInit(command) {
        const info = await core.getDeviceInfo();
        // check device is well connected and can be opened
        if (info.code !== core.constants.rets.SUCCESS) {
            console.log(`get device info failed: ${utils.parseReturnCode(info.code)} `);
            return;
        } else {
            // check device is able to init
            if (info.result.ucLifeCycle !== core.constants.devinfo.LIFECYCLE_AGREE) {
                console.log(`init failed: device lifecycle is ${utils.parseLifeCycle(info.result.ucLifeCycle)}`);
                return;
            }
        }
        let result ={};
        switch (command[1]) {
            case 'generate':
                result = await core.generateSeed(parseInt(command[2]));
                break;
            case 'import':
                result = await core.importSeed();
                break;
            default:
                console.log(`unknown parameter: ${command[1]} `);
                break;
        }
        if (result.code === core.constants.rets.SUCCESS) {
            console.log(`${command[1]} completed successfully`);
        } else {
            console.log(`${command[1]} failed: ${utils.parseReturnCode(result.code)} `);
        }
    }
    ```
2. Edit the `init` branch inside the `switch` statement in `index.js`:
   
    ```js
    case 'init':
        await processInit(command);
        break;
    ```

3. Now you have finished this section, make sure your **WOOKONG Solo** is well connected and not initialized, run `node index.js` and run `init` under `WST>` prompt to initialize your **WOOKONG Solo** for the next section. For generating new seed, please backup the mnemonic words  displayed on **WOOKONG Solo** carefully, after clicking the ‘OK’ button, **WOOKONG Solo** will ask you to input 2 words (which selected randomly from the mnemonic words) to check if you have backed up correctly, for importing existed, select mnemonic count on **WOOKONG Solo** first, then input them on **WOOKONG Solo** and press ‘OK’ to execute importing.