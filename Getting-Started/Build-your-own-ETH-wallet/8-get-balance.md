# Get balance[optional]

## `balance` command


In this section, we will get ETH balance of the ETH address we've got from **WOOKONG Solo**.

1. To get ETH balance, we should import another package. Run `npm i web3` to install [web3.js](https://github.com/ethereum/web3.js).
   
2. Add the following code at the top of `index.js`.
    ```js
    const Web3 = require('web3');

    const NODE_URL = 'https://mainnet.infura.io'; // https://mainnet-eth.token.im is also available

    const web3 = new Web3(new Web3.providers.HttpProvider(NODE_URL));
    ```
3. Add the following function at the end of `index.js`, we do not need to show address on device screen here, so the last parameter of getAddress should be **0** according to the [API document](../API/api.md#getaddresscointype-derivepath-showonscreen).
    ```js
    async function processGetBalance(command) {
        const ready = await isDeviceReady();
        if (!ready) {
            return;
        }
        //get address
        const derivePath = JSON.parse(command[1]);
        const result = await getAddress(derivePath, 0);
        if (result.code !== core.constants.rets.SUCCESS) {
            console.log(`get address failed: ${utils.parseReturnCode(result.code)} `);
            return;
        }
        //get balance by address
        try {
            const balanceInWei = await web3.eth.getBalance(result.result.address);
            //balance is returned in Wei, so we need to transform to Ether
            const balanceInEther = web3.utils.fromWei(balanceInWei);
            console.log(`your ETH address is: ${result.result.address}, balance is: ${balanceInEther.toString()} Ether`);
        } catch (error) {
            console.log(`error: ${error.message}`);
            return;
        }
    }
    ```
4. Now connect your **WOOKONG Solo** to your system, make sure it is well connected and unlocked, run `node index.js`, then run `balance -p[0, 2147483692, 2147483708, 2147483648, 0, 0]` under `WST>` prompt, you may see output as shown below:

    ```shell
    WST> balance [0,2147483692,2147483708,2147483648,0]
    your ETH address is: 0x7F825230F5F2A26523999c98e0E3f7E2697085A9, balance is: 0.00001 Ether
    ```