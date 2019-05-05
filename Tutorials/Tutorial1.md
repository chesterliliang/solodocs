# `info` command

**Intergrate **wookong-solo-lib** into current project and get device info of connected **WOOKONG Solo****

In tutorial 1, we will intergrate **wookong-solo-lib** into the project, and try to get device info from connected **WOOKONG Solo**.


1. type `npm install https://github.com/extropiescom/wookong-solo-lib --save` in command line and run it.

2. Add this line to the top of `index.js`：
   
    ```js
    const core = require('wookong-solo-lib');
    ```
3. Now we can use all functions provided by **wookong-solo-lib**, let's try to get device info, edit the `info` branch inside the `switch` statement in `index.js`:
   
    ```js
    case 'info':
        const devInfo = await core.getDeviceInfo();
        console.log('devInfo: ', devInfo);
        break;
    ```

4. Connect your **WOOKONG Solo** to your system, and run `node index.js`, then run `info` under the `WST>` prompt, you may see output like this:
    ```shell
    WST> info
    devInfo:  { code: 0,
    result:
    { ucPINState: 0,
        ucCOSType: 1,
        ucChainType: 1,
        pbSerialNumber: '2018102600001',
        pbCOSVersion: [ 1, 1, 0, 28 ],
        ucLifeCycle: 2,
        nLcdState: 1024,
        pbSessKeyHash: [ 0, 0, 0, 0 ],
        nN: 0,
        nT: 0,
        pbBLEVersion: [ 0, 0, 0, 0 ] } }
    ```
5. Now we have successfully got the device info of **WOOKONG Solo**, but it is not clearly enough for us to read, so we can make a little change to make the ouputs more readable.
   
    5.1 Create a new file with name `util.js` under the same level of `index.js`, and fill it with the following content, which comes from [API-core.constants](../API/api.md#coreconstants).

    ```js
    const { constants } = require('wookong-solo-lib');

    function parseReturnCode(code) {
        switch(code) {
            case constants.rets.SUCCESS:
                return 'success'; 
            case constants.rets.UNKNOWN_FAIL:
                return 'unknown failure'; 
            case constants.rets.ARGUMENTBAD:
                return 'argument bad'; 
            case constants.rets.HOST_MEMORY:
                return 'malloc memory failed'; 
            case constants.rets.DEV_ENUM_FAIL:
                return 'enum device failed'; 
            case constants.rets.DEV_OPEN_FAIL:
                return 'open device failed'; 
            case constants.rets.DEV_COMMUNICATE_FAIL:
                return 'communicate failed'; 
            case constants.rets.DEV_NEED_PIN:
                return 'device need user input pin to "unlock"'; 
            case constants.rets.DEV_OP_CANCEL:
                return 'operation canceled'; 
            case constants.rets.DEV_KEY_NOT_RESTORED:
                return 'operation need seed restored while current state is not restored'; 
            case constants.rets.DEV_KEY_ALREADY_RESTORED:
                return 'seed already restored'; 
            case constants.rets.DEV_COUNT_BAD:
                return 'errors such as no device, or device count must equal to N when init, device count must >=T and <=N when restore or sign'; 
            case constants.rets.DEV_RETDATA_INVALID:
                return 'received data length less than 2 or ret data structure invalid'; 
            case constants.rets.DEV_AUTH_FAIL:
                return 'device authentication failed'; 
            case constants.rets.DEV_STATE_INVALID:
                return 'life cycle or other device state not matched to current operation'; 
            case constants.rets.DEV_WAITING:
                return 'device waiting'; 
            case constants.rets.DEV_COMMAND_INVALID:
                return 'command can not recognized by device'; 
            case constants.rets.DEV_RUN_COMMAND_FAIL:
                return 'received data not 9000'; 
            case constants.rets.DEV_HANDLE_INVALID:
                return 'device handle invalid'; 
            case constants.rets.COS_TYPE_INVALID:
                return 'device cos type value must be DEV_INFO_COS_TYPE_XXX'; 
            case constants.rets.COS_TYPE_NOT_MATCH:
                return 'device cos type not matched to current operation, such as dragon ball spec function calls personal e-wallet, or passed argument implies specific cos type while current cos type not match, or current insert devices\' types are not the same'; 
            case constants.rets.DEV_BAD_SHAMIR_SPLIT:
                return 'bad shamir split'; 
            case constants.rets.DEV_NOT_ONE_GROUP:
                return 'dragon ball device is not belong to one group'; 
            case constants.rets.BUFFER_TOO_SAMLL:
                return 'size of input buffer not enough to store return data'; 
            case constants.rets.TX_PARSE_FAIL:
                return 'input transaction parse failed'; 
            case constants.rets.TX_UTXO_NEQ:
                return 'count of input and UTXO is not equal'; 
            case constants.rets.TX_INPUT_TOO_MANY:
                return 'input count shouldn\'t larger than 100'; 
            case constants.rets.MUTEX_ERROR:
                return 'mutex error, such as create/free/lock/unlock'; 
            case constants.rets.COIN_TYPE_INVALID:
                return 'value of coin type must be COIN_TYPE_XXX'; 
            case constants.rets.COIN_TYPE_NOT_MATCH:
                return 'value of coin type must be equal to the value passed to DeriveTradeAddress'; 
            case constants.rets.DERIVE_PATH_INVALID:
                return 'derive path must start by 0x00000000, indicates m'; 
            case constants.rets.NOT_SUPPORTED:
                return 'call not supported'; 
            case constants.rets.INTERNAL_ERROR:
                return 'library internal errors, such as internal structure definition mistake'; 
            case constants.rets.BAD_N_T:
                return 'value of N or T is invalid'; 
            case constants.rets.TARGET_DEV_INVALID:
                return 'when getting address or signing, dragon ball must select a target device by calling DeriveTradeAddress successfully first'; 
            case constants.rets.CRYPTO_ERROR:
                return 'crypto error'; 
            case constants.rets.DEV_TIMEOUT:
                return 'operation time out'; 
            case constants.rets.DEV_PIN_LOCKED:
                return 'PIN locked'; 
            case constants.rets.DEV_PIN_CONFIRM_FAIL:
                return 'set new pin error when confirm'; 
            case constants.rets.DEV_PIN_VERIFY_FAIL:
                return 'input pin error when change pin or do other operation'; 
            case constants.rets.DEV_CHECKDATA_FAIL:
                return 'input data check failed in device, usually caused by invalid CRC check'; 
            case constants.rets.DEV_DEV_OPERATING:
                return 'user is operating device, please wait'; 
            case constants.rets.DEV_PIN_UNINIT:
                return 'PIN not initialized'; 
            case constants.rets.DEV_BUSY:
                return 'device is busy, such as when enroll or verify finger print, previous operation is not finished yet'; 
            case constants.rets.DEV_ALREADY_AVAILABLE:
                return 'device is available, not need to abort again'; 
            case constants.rets.DEV_DATA_NOT_FOUND:
                return 'required data is not found'; 
            case constants.rets.DEV_SENSOR_ERROR:
                return 'sensor (such as finger print sensor) error'; 
            case constants.rets.DEV_STORAGE_ERROR:
                return 'device storage error'; 
            case constants.rets.DEV_STORAGE_FULL:
                return 'device storage full'; 
            case constants.rets.DEV_FP_COMMON_ERROR:
                return 'finger print common error (such as finger print verify or enroll error)'; 
            case constants.rets.DEV_FP_REDUNDANT:
                return 'finger print redundant error'; 
            case constants.rets.DEV_FP_GOOG_FINGER:
                return 'finger print enroll step success'; 
            case constants.rets.DEV_FP_NO_FINGER:
                return 'sensor haven\'t got any finger print'; 
            case constants.rets.DEV_FP_NOT_FULL_FINGER:
                return 'sensor haven\'t got full finger print image'; 
            case constants.rets.DEV_FP_BAD_IMAGE:
                return 'sensor haven\'t got valid image'; 
            case constants.rets.DEV_LOW_POWER:
                return 'device power is too low'; 
            case constants.rets.DEV_TYPE_INVALID:
                return 'invalid device type'; 
            case constants.rets.NO_VERIFY_COUNT:
                return 'count of verification run out when doing signature'; 
            case constants.rets.AUTH_CANCEL:
                return 'not used yet'; 
            case constants.rets.PIN_LEN_ERROR:
                return 'PIN length error'; 
            case constants.rets.AUTH_TYPE_INVALID:
                return 'authenticate type invalid'; 
            case constants.rets.DEV_FUNC_INVALID:
                return 'user-defined device function invalid';
            default:
                return `unknown return code: ${code}`;
        }
    }

    function parsePINState(state) {
        switch (state) {
            case constants.devinfo.PIN_INVALID_STATE:
                return 'PIN state is: invalid state';
            case constants.devinfo.PIN_LOGOUT:
                return 'PIN state is: logged out';
            case constants.devinfo.PIN_LOGIN:
                return 'PIN state is: logged in';
            case constants.devinfo.PIN_LOCKED:
                return 'PIN state is: locked';
            case constants.devinfo.PIN_UNSET:
                return 'PIN state is: unset, should set pin first';
            default:
                return `unknown PIN state: ${state}`;
        }
    }

    function parseChainType(chainType) {
        switch (chainType) {
            case constants.devinfo.CHAIN_TYPE_FORMAL:
                return 'chain type is: formal net';
            case constants.devinfo.CHAIN_TYPE_TEST:
                return 'chain type is: test net';
            default:
                return `unknown chain type: ${chainType}`;
        }
    }

    function parseLifeCycle(lifeCycle) {
        switch (lifeCycle) {
            case constants.devinfo.LIFECYCLE_INVALID:
                return 'lifecycle is: invalid';
            case constants.devinfo.LIFECYCLE_AGREE:
                return 'lifecycle is: seed not generated';
            case constants.devinfo.LIFECYCLE_USER:
                return 'lifecycle is: normal state, seed generated';
            case constants.devinfo.LIFECYCLE_PRODUCE:
                return 'lifecycle is: producting state, reserved';
            default:
                return `unknown lifecycle: ${lifeCycle}`;
        }
    }

    function parseLcdState(state) {
        switch (state) {
            case constants.devinfo.LCD_NULL:
                return 'lcd state is: normal state';
            case constants.devinfo.LCD_SHOWLOGO:
                return 'lcd state is: logo is shown on screen';
            case constants.devinfo.LCD_WAITTING:
                return 'lcd state is: waiting is shown on screen';
            case constants.devinfo.LCD_SHOWOK:
                return 'lcd state is: OK is shown on screen';
            case constants.devinfo.LCD_SHOWCANCEL:
                return 'Lifecycle is: Cancel is shown on screen';
            case constants.devinfo.LCD_SHOWSKEYHASH:
                return 'lcd state is: Session key hash is shown on screen';
            case constants.devinfo.LCD_SHOWADDRESS:
                return 'lcd state is: coin address is shown on screen';
            case constants.devinfo.LCD_SHOWBTCSIGN:
                return 'lcd state is: btc sign info is shown on screen';
            case constants.devinfo.LCD_SHOWETHSIGN:
                return 'Lifecycle is: eth sign info is shown on screen';
            case constants.devinfo.LCD_SETNEWPIN:
                return 'Lifecycle is: set new pin is shown on screen';
            case constants.devinfo.LCD_CHANGEPIN:
                return 'lcd state is: change pin is shown on screen';
            case constants.devinfo.LCD_VERIFYPIN:
                return 'lcd state is: verify pin is shown on screen';
            case constants.devinfo.LCD_WAITTING:
                return 'lcd state is: verify pin is shown on screen';
            case constants.devinfo.LCD_PINLOCKED:
                return 'lcd state is: pin locked is shown on screen';
            case constants.devinfo.LCD_FORMAT:
                return 'Lifecycle is: format is shown on screen';
            case constants.devinfo.LCD_REBOOT:
                return 'lcd state is: eboot is shown on screen';
            case constants.devinfo.LCD_SHOWBIP39:
                return 'lcd state is: bip39 mnemonics are show on screen';
            case constants.devinfo.LCD_CHECKBIP39:
                return 'lcd state is: check bip39 mnemonics input is shown on screen';
            case constants.devinfo.LCD_SHOWBTSSIGN:
                return 'lcd state is: CYB sign info is shown on screen';
            case constants.devinfo.LCD_PINERROR:
                return 'lcd state is: pin error is shown on screen';
            case constants.devinfo.LCD_SHOWM:
                return 'lcd state is: M is shown on screen';
            case constants.devinfo.LCD_SHOWTIMEOUT:
                return 'lcd state is: timeout is shown on screen';
            case constants.devinfo.LCD_SHOWEOSSIGN:
                return 'lcd state is: eos sign info is shown on screen';
            case constants.devinfo.LCD_SHOWFAIL:
                return 'lcd state is: fail is shown on screen';
            case constants.devinfo.LCD_SHOWNEOSIGN:
                return 'lcd state is: neo sign info is show on screen';
            case constants.devinfo.LCD_WAITING_TIMEOUT:
                return 'lcd state is: waiting timeout is shown on screen';
            case constants.devinfo.LCD_GET_MNENUM:
                return 'lcd state is: getting mnemonics number is shown on screen';
            case constants.devinfo.LCD_GETMNE_BYDEV:
                return 'lcd state is: getting mnemonics is shown on screen';
            default:
                return `unknown lcd state: ${state}`;
        }
    }

    module.exports = {
        parseReturnCode,
        parsePINState,
        parseChainType,
        parseLifeCycle,
        parseLcdState
    }
    ```

    5.2 Add the following code to the top of `index.js`.

    ```js
    const utils = require('./utils');
    ```

    5.3 We should create a function to process the `info` command, add the following code to the end of `index.js`.
    
    ```js
    async function processGetDeviceInfo() {
        const info = await core.getDeviceInfo();
        if (info.code === core.constants.rets.SUCCESS ) {
            console.log(utils.parsePINState(info.result.ucPINState));
            console.log(utils.parseChainType(info.result.ucChainType));
            console.log(`device sn: ${info.result.pbSerialNumber}`);
            console.log(`device firmware version: ${info.result.pbCOSVersion.toString()}`, );
            console.log(utils.parseLifeCycle(info.result.ucLifeCycle));
            console.log(utils.parseLcdState(info.result.nLcdState));
        } else {
            console.log(`get device info failed: ${utils.parseReturnCode(info.code)} `);
        }
    }
    ```

    5.4 Now we can modify the code for the `info` branch in the `switch` statement in `index.js`.
    
    ```js
    case 'info':
        await processGetDeviceInfo();
        break;
    ```

6. Now you have finished tutorial 01, make sure your **WOOKONG Solo** is well connected, run `node index.js` and run `info` under `WST>` prompt, then you will see output like this:
   
    ```shell
    WST> info
    PIN state is: logged out
    chain type is: formal net
    Device sn: 2018102600001
    Device firmware version: 1,1,0,28
    lifecycle is: normal state, seed generated
    lcd state is: verify pin is shown on screen
    ```