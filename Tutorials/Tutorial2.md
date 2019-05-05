# `addr` command

**Get your ETH address from **WOOKONG Solo****

In tutorial 2, we will get a ETH address from connected **WOOKONG Solo**, according to [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md), use `[0, 2147483692, 2147483708, 2147483648, 0, 0]` (indicates `[0, 0x8000002c, 0x8000003c, 0x80000000, 0x00000000]` in decimal) as the derive path for ETH is strongly recommended in the whole tutorials.

1. Add the following function to the end of `index.js`, we need to show address on device screen, so the last parameter of `getAddress(coinType, derivePath, showOnScreen)` should be **1** according to the [API document](../API/api.md#getaddresscointype-derivepath-showonscreen).
   
    ```js
    async function processGetAddress(command) {
        const derivePath = JSON.parse(command[1]);
        const result = await core.getAddress(core.constants.coins.COIN_TYPE_ETH, derivePath, 1);
        if (result.code === core.constants.rets.SUCCESS) {
            console.log(`your ETH address is: ${result.result.address} `);
        } else {
            console.log(`get address failed: ${utils.parseReturnCode(result.code)} `);
        }
    }
    ```

2. Modify the code of `addr` branch in `switch` statement in `index.js` to the following code:

    ```js
    case 'addr':
        await processGetAddress(command);
        break;
    ```

3. Now connect your **WOOKONG Solo** to your system and keep it locked, run `node index.js`, then run `addr -p[0, 2147483692, 2147483708, 2147483648, 0, 0]` under `WST>` prompt, you may see output as shown below:

    ```shell
    WST> addr -p[0, 2147483692, 2147483708, 2147483648, 0, 0]
    get address failed: device need user input pin to "unlock" 
    ```

4. Input the right pin on your **WOOKONG Solo** to unlock it, run `addr -p[0, 2147483692, 2147483708, 2147483648, 0, 0]` again under `WST>` prompt, watch your **WOOKONG Solo**'s screen, press 'OK' button when the screen shows ETH address, then you may see output as shown below:
    ```shell
    WST> addr -p[0, 2147483692, 2147483708, 2147483648, 0, 0]
    your ETH address is: 0x7F825230F5F2A26523999c98e0E3f7E2697085A9 
    ```
5. Now the basic feature of get address command is completed, but as we tried on step 2, operations to **WOOKONG Solo** may fail if **WOOKONG Solo** is locked, this is described in [API Document](../API/api.md#functions), so it is better to check device state before every operation. Add the following code to the end of `index.js`.
    ```js
    async function isDeviceReady() {
        const result = await core.getDeviceInfo();
        if (result.code !== core.constants.rets.SUCCESS) {
            console.log(`get device info failed: ${utils.parseReturnCode(result.code)} `);
            return false;
        } else {
            if (result.result.ucPINState !== core.constants.devinfo.PIN_LOGIN) {
                console.log(`invalid PIN state, please unlock PIN first`);
                return false;
            } 
            if (result.result.nLcdState !== core.constants.devinfo.LCD_NULL && result.result.nLcdState !== core.constants.devinfo.LCD_SHOWLOGO) {
                console.log(`invalid lcd state, please ensure LCD is showing WOOKONG first`);
                return false;
            }
            return true;
        }
    }
    ```
6. Add the following code at the beginning to the body of `processGetAddress(command)`.
    ```js
    const ready = await isDeviceReady();
    if (!ready) {
        return;
    }
    ```

7. `balance` command and `send` command also need to get address first, so it is better to use a function to get address, add the following function to the end of `index.js`.
    ```js
    async function getAddress(derivePath, showOnScreen) {
        const result = await core.getAddress(core.constants.coins.COIN_TYPE_ETH, derivePath, showOnScreen);
        return result;
    }
    ```
8. Modify function `processGetAddress(command)` to the following code.
    ```js
    async function processGetAddress(command) {
        const ready = await isDeviceReady();
        if (!ready) {
            return;
        }
        const derivePath = JSON.parse(command[1]);
        const result = await getAddress(derivePath, 1);
        if (result.code === core.constants.rets.SUCCESS) {
            console.log(`your ETH address is: ${result.result.address} `);
        } else {
            console.log(`get address failed: ${utils.parseReturnCode(result.code)} `);
        }
    }
    ```
9.  `addr` command is implemented, you should transfer some ETH to the address you've just got for the next tutorials.