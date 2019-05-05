# Firmware update procedure
 
The whole firmware update procedure may be divided into two steps:
1. Erase current existing user firmware by calling [<code>clearCOS()</code>](./4Functions.md#clearCOS)
   
2. Make sure user firmware of connected **WOOKONG Solo** device had been erased successfully, then call [<code>updateCOS(cosData, callback)</code>](./4Functions.md#updatecoscosdata-callback)

Notice: [<code>clearCOS()</code>](./4Functions.md#clearCOS) and [<code>updateCOS(cosData, callback)</code>](./4Functions.md#updatecoscosdata-callback) may result device communication fail on some version of OS, e.g: macOS High Sierra (10.13), so when you got a code that is not equal to [<code>DEV_COMMAND_INVALID</code>](./3core.constants.md#coreconstantsrets) returned by getDeviceInfo(), you should try to disconnect and reconnect **WOOKONG Solo**.


**Example**  
```js

let ret = await core.getDeviceInfo();
if (ret.code === constants.rests.SUCCESS) {
    // user firmware exists, should clear first
    if (&& ret.result.ucPINState === constants.devinfo.PIN_LOG_IN && (ret.result.nLcdState === constants.devinfo.LCD_NULL || ret.result.nLcdState === constants.devinfo.LCD_SHOWLOGO)) {
        ret = await core.clearCOS();
        if (ret.code !== constants.rests.SUCCES) {
            // clear user firmware failed, procedure should stop here
            return FAIL;
        }
        ret = await core.getDeviceInfo();
        if (ret.code !== constants.rests.SUCCES) {
            // user firmware was erased successfully, but could not connect to device now, 
            // MUST prompt users to disconnect device and reconnect, then try again
            return NEED_RECONNECT;
        }
    } else {
        // device status does not meet the requirements of clearCOS()
        // MUST prompt users to make sure device is well connected, unlocke the device and try again
        return FAIL;
    }    
} else if (ret.code !== constants.rests.DEV_COMMAND_INVALID) {
    // could not get device info, and the return value does not show that user firmware had been erased.
    // MUST prompt users to make sure device is well connected, unlocke the device and try again
    return FAIL;
}

const callback = (progress) => console.log('progress', progress);
ret = await core.updateCOS(cosData, callback);
if (ret.code !== constants.rests.SUCCES) {
    // update user firmware failed
    return FAIL;
}

ret = await core.getDeviceInfo();
if (ret.code !== constants.rests.SUCCES) {
    // user firmware was updated successfully, but could not connect to device now, 
    // MUST prompt users to disconnect device and reconnect, then try again
    return NEED_RECONNECT;
}
return SUCCESS;
```