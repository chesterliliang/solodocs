# Clear your **WOOKONG Solo**

## `format` command

**WOOKONG Solo** is reusable, but before you re-initialize your **WOOKONG Solo**, you must format it first. We will implement `format` command in this section.

Before formatting **WOOKONG Solo**, **MAKE SURE** you have saved your mnemonics already or the balance of your address from **WOOKONG Solo** is 0. **FORMAT is a dagerous operation that may cause loss of your digital assets**, please make sure you know what you are doing.


1. Use [format()](./4-Functions.md#format) to format your **WOOKONG Solo**. Add the following function to the end of `index.js`.
   
    ```js
    async function processFormat() {
    const info = await core.getDeviceInfo();
    // check device is well connected and can be opened
    if (info.code !== core.constants.rets.SUCCESS) {
        console.log(`get device info failed: ${utils.parseReturnCode(info.code)} `);
        return;
    }
    const result = await core.format();
    if (result.code === core.constants.rets.SUCCESS) {
        console.log(`format completed successfully`);
    } else {
        console.log(`format failed: ${utils.parseReturnCode(result.code)} `);
    }
}
    ```
2. Edit the `format` branch inside the `switch` statement in `index.js`:
   
    ```js
    case 'format':
        await processFormat(command);
        break;
    ```

3. Now you have finished this section, connect your **WOOKONG Solo** to your system and make sure your have saved your mnemonics already, run `node index.js` and run `init` under `WST>` prompt to format your **WOOKONG Solo**, but rember to init it again for the next section.