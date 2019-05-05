# API references

## Table of contents

- [API references](#api-references)
  - [Table of contents](#table-of-contents)
  - [Usage](#usage)
  - [core.constants](#coreconstants)
    - [core.constants.rets](#coreconstantsrets)
    - [core.constants.coins](#coreconstantscoins)
    - [core.constants.lengths](#coreconstantslengths)
    - [core.constants.devinfo](#coreconstantsdevinfo)
      - [PIN status definition](#pin-status-definition)
      - [Chain type definition](#chain-type-definition)
      - [Firmware version length definition](#firmware-version-length-definition)
      - [Firmware type definition](#firmware-type-definition)
      - [Lifecycle definition](#lifecycle-definition)
      - [LCD status definition](#lcd-status-definition)
      - [Others definition](#others-definition)
  - [Functions](#functions)
    - [getDeviceInfo()](#getdeviceinfo)
    - [getDeviceCount() ⇒](#getdevicecount-%E2%87%92)
    - [changePIN()](#changepin)
    - [format()](#format)
    - [getAddress(coinType, derivePath, showOnScreen)](#getaddresscointype-derivepath-showonscreen)
    - [generateSeed(seedLen)](#generateseedseedlen)
    - [importSeed()](#importseed)
    - [getLibraryVersion()](#getlibraryversion)
    - [signBTC(derivePath, currentTX, utxos)](#signbtcderivepath-currenttx-utxos)
    - [signLTC(derivePath, currentTX, utxos)](#signltcderivepath-currenttx-utxos)
    - [signNEO(derivePath, currentTX, utxos)](#signneoderivepath-currenttx-utxos)
    - [signEthereum(derivePath, currentTX, isETH, erc20Info)](#signethereumderivepath-currenttx-iseth-erc20info)
    - [signCYB(derivePath, currentTX)](#signcybderivepath-currenttx)
    - [signEOS(derivePath, currentTX)](#signeosderivepath-currenttx)
    - [signXRP(derivePath, currentTX)](#signxrpderivepath-currenttx)
    - [getPubKey(derivePath, coinType)](#getpubkeyderivepath-cointype)
    - [clearCOS()](#clearcos)
    - [updateCOS(cosData, callback)](#updatecoscosdata-callback)
    - [verifyFileSignature()](#verifyfilesignature)
  - [Function result objects](#function-result-objects)
    - [getDeviceInfoResult](#getdeviceinforesult)
    - [getDeviceCountResult](#getdevicecountresult)
    - [getAddressResult](#getaddressresult)
    - [signBTCResult](#signbtcresult)
    - [signLTCResult](#signltcresult)
    - [signNEOResult](#signneoresult)
    - [signEthereumResult](#signethereumresult)
    - [signCYBResult](#signcybresult)
    - [signEOSResult](#signeosresult)
    - [signXRPResult](#signxrpresult)
    - [getPubKeyResult](#getpubkeyresult)
  - [Firmware update procedure](#firmware-update-procedure)

## Usage
Use the following code to import **wookong-solo-lib**

`import core from 'wookong-solo-lib'`

or

`const core = require('wookong-solo-lib')`

## core.constants
core.constants is collection of constants may be used in fuctions as parameters or return
### core.constants.rets
| Name | Value | Description |
| --- | --- | --- |
| SUCCESS | 0x00000000 | success |
| UNKNOWN_FAIL | 0x80000001 | unknown failure |
| ARGUMENTBAD | 0x80000002 | argument bad |
| HOST_MEMORY | 0x80000003 | malloc memory failed |
| DEV_ENUM_FAIL | 0x80000004 | enum device failed |
| DEV_OPEN_FAIL | 0x80000005 | open device failed |
| DEV_COMMUNICATE_FAIL | 0x80000006 | communicate failed |
| DEV_NEED_PIN | 0x80000007 | device need user input pin to "unlock" |
| DEV_OP_CANCEL | 0x80000008 | operation canceled |
| DEV_KEY_NOT_RESTORED | 0x80000009 | operation need seed restored while current state is not restored |
| DEV_KEY_ALREADY_RESTORED | 0x8000000a | seed already restored |
| DEV_COUNT_BAD | 0x8000000b | errors such as no device, or device count must equal to N when init, device count must >=T and <=N when restore or sign |
| DEV_RETDATA_INVALID | 0x8000000c | received data length less than 2 or ret data structure invalid |
| DEV_AUTH_FAIL | 0x8000000d | device authentication failed |
| DEV_STATE_INVALID | 0x8000000e | life cycle or other device state not matched to current operation |
| DEV_WAITING | 0x8000000f | device waiting |
| DEV_COMMAND_INVALID | 0x80000010 | command can not recognized by device |
| DEV_RUN_COMMAND_FAIL | 0x80000011 | received data not 9000 |
| DEV_HANDLE_INVALID | 0x80000012 | device handle invalid |
| COS_TYPE_INVALID | 0x80000013 | device cos type value must be DEV_INFO_COS_TYPE_XXX |
| COS_TYPE_NOT_MATCH | 0x80000014 | device cos type not matched to current operation, such as dragon ball spec function calls personal e-wallet, or passed argument implies specific cos type while current cos type not match, or current insert devices' types are not the same |
| DEV_BAD_SHAMIR_SPLIT | 0x80000015 | bad shamir split |
| DEV_NOT_ONE_GROUP | 0x80000016 | dragon ball device is not belong to one group |
| BUFFER_TOO_SAMLL | 0x80000017 | size of input buffer not enough to store return data |
| TX_PARSE_FAIL | 0x80000018 | input transaction parse failed |
| TX_UTXO_NEQ | 0x80000019 | count of input and UTXO is not equal |
| TX_INPUT_TOO_MANY | 0x8000001a | input count shouldn't larger than 100 |
| MUTEX_ERROR | 0x8000001b | mutex error, such as create/free/lock/unlock |
| COIN_TYPE_INVALID | 0x8000001c | value of coin type must be COIN_TYPE_XXX |
| COIN_TYPE_NOT_MATCH | 0x8000001d | value of coin type must be equal to the value passed to DeriveTradeAddress |
| DERIVE_PATH_INVALID | 0x8000001e | derive path must start by 0x00000000, indicates m |
| NOT_SUPPORTED | 0x8000001f | call not supported |
| INTERNAL_ERROR | 0x80000020 | library internal errors, such as internal structure definition mistake |
| BAD_N_T | 0x80000021 | value of N or T is invalid |
| TARGET_DEV_INVALID | 0x80000022 | when getting address or signing, dragon ball must select a target device by calling DeriveTradeAddress successfully first |
| CRYPTO_ERROR | 0x80000023 | crypto error |
| DEV_TIMEOUT | 0x80000024 | operation time out |
| DEV_PIN_LOCKED | 0x80000025 | PIN locked |
| DEV_PIN_CONFIRM_FAIL | 0x80000026 | set new pin error when confirm |
| DEV_PIN_VERIFY_FAIL | 0x80000027 | input pin error when change pin or do other operation |
| DEV_CHECKDATA_FAIL | 0x80000028 | input data check failed in device, usually caused by invalid CRC check |
| DEV_DEV_OPERATING | 0x80000029 | user is operating device, please wait |
| DEV_PIN_UNINIT | 0x8000002a | PIN not initialized |
| DEV_BUSY | 0x8000002b | device is busy, such as when enroll or verify finger print, previous operation is not finished yet |
| DEV_ALREADY_AVAILABLE | 0x8000002c | device is available, not need to abort again |
| DEV_DATA_NOT_FOUND | 0x8000002d | required data is not found |
| DEV_SENSOR_ERROR | 0x8000002e | sensor (such as finger print sensor) error |
| DEV_STORAGE_ERROR | 0x8000002f | device storage error |
| DEV_STORAGE_FULL | 0x80000030 | device storage full |
| DEV_FP_COMMON_ERROR | 0x80000031 | finger print common error (such as finger print verify or enroll error) |
| DEV_FP_REDUNDANT | 0x80000032 | finger print redundant error |
| DEV_FP_GOOG_FINGER | 0x80000033 | finger print enroll step success |
| DEV_FP_NO_FINGER | 0x80000034 | sensor haven't got any finger print |
| DEV_FP_NOT_FULL_FINGER | 0x80000035 | sensor haven't got full finger print image |
| DEV_FP_BAD_IMAGE | 0x80000036 | sensor haven't got valid image |
| DEV_LOW_POWER | 0x80000037 | device power is too low |
| DEV_TYPE_INVALID | 0x80000038 | invalid device type |
| NO_VERIFY_COUNT | 0x80000039 | count of verification run out when doing signature |
| AUTH_CANCEL | 0x8000003a | not used yet |
| PIN_LEN_ERROR | 0x8000003b | PIN length error |
| AUTH_TYPE_INVALID | 0x8000003c | authenticate type invalid |
| DEV_FUNC_INVALID | 0x8000003d | user-defined device function invalid

### core.constants.coins

| Name | Value | Description |
| --- | --- | --- |
| COIN_TYPE_BTC | 0x00 |  |
| COIN_TYPE_ETH | 0x01 |  |
| COIN_TYPE_CYB | 0x02 |  |
| COIN_TYPE_EOS | 0x03 |  |
| COIN_TYPE_LTC | 0x04 |  |
| COIN_TYPE_NEO | 0x05 |  |
| COIN_TYPE_ETC | 0x06 |  |
| COIN_TYPE_XRP | 0x09 |  |
| COIN_TYPE_USDT | 0x0A |  |

### core.constants.lengths

| Name | Value | Description |
| --- | --- | --- |
| MAX_LEN_BTC_SIG | 112 | max length of BTC signature |
| MAX_LEN_LTC_SIG | 112 | max length of LTC signature |
| MAX_LEN_NEO_SIG | 112 | max length of NEO signature |
| MAX_LEN_CYB_SIG | 65 | max length of CYB signature |
| MAX_LEN_ETH_SIG | 69 | max length of ETH signature |
| MAX_LEN_XRP_SIG | 112 | max length of XRP signature |
| MAX_LEN_EOS_SIG | 256 | max length of EOS signature |
| MAX_LEN_SIG | | MAX_LEN_EOS_SIG | max length of coin signatures |
| MAX_LEN_PUBKEY | 96 | max length of coin public key |
| MAX_LEN_ADDR | 0x80 | max length of coin addresss |
| DEVICE_CHECK_CODE_LEN | 0x50 | length of hardware device check code |
| PROC_MSG| 256 | reserved |

### core.constants.devinfo

#### PIN status definition

| Name | Value | Description |
| --- | --- | --- |
| PIN_INVALID_STATE | 0xFF | PIN in a invalid state |
| PIN_LOGOUT | 0x00 | PIN status is logged out |
| PIN_LOGIN | 0x01 | PIN status is logged in |
| PIN_LOCKED | 0x02 | PIN is locked |
| PIN_UNSET | 0x03 | PIN is unset, should set pin first |

#### Chain type definition

| Name | Value | Description |
| --- | --- | --- |
| CHAIN_TYPE_FORMAL | 0x01 | chain type of device is formal net |
| CHAIN_TYPE_TEST | 0x02 | chain type of device is test net |

#### Firmware version length definition

| Name | Value | Description |
| --- | --- | --- |
| COS_VERSION_LEN | 0x04 | length of firmware version |
| BLE_VERSION_LEN | 0x04 | length of ble version |

#### Firmware type definition

| Name | Value | Description |
| --- | --- | --- |
| COS_TYPE_INDEX | 0x01 | reserved  |
| COS_TYPE_INVALID | 0xFF | firmware type is invalid |
| COS_TYPE_DRAGONBALL | 0x00 | firmware type is **WOOKONG Enterprise** |
| COS_TYPE_PERSONAL | 0x01 | firmware type is **WOOKONG Solo** |
| COS_TYPE_BIO | 0x02 | firmware type is **WOOKONG Bio** |

#### Lifecycle definition

| Name | Value | Description |
| --- | --- | --- |
| LIFECYCLE_INVALID | 0xFF | lifecycle is invalid |
| LIFECYCLE_AGREE | 0x01 | seed not generated |
| LIFECYCLE_USER | 0x02 | normal state, seed generated |
| LIFECYCLE_PRODUCE | 0x04 | producting state, reserved |

#### LCD status definition

Make sure device LCD state is LCD_NULL or LCD_SHOWLOGO before operations, otherwise you may get constants.rets.DEV_DEV_OPERATING(0x80000029)

| Name | Value | Description |
| --- | --- | --- |
| LCD_NULL | 0x00000000 | nothing is shown on screen |
| LCD_SHOWLOGO | 0x00000001 | logo is shown on screen |
| LCD_WAITTING | 0x00000002 | waiting is shown on screen |
| LCD_SHOWOK | 0x00000004 | OK is shown on screen |
| LCD_SHOWCANCEL | 0x00000008 | Cancel is shown on screen |
| LCD_SHOWSKEYHASH | 0x00000010 | Session key hash is shown on screen, reserved |
| LCD_SHOWADDRESS | 0x00000020 | coin address is shown on screen |
| LCD_SHOWBTCSIGN | 0x00000040 | btc sign info is shown on screen |
| LCD_SHOWETHSIGN | 0x00000080 | eth sign info is shown on screen |
| LCD_SETNEWPIN | 0x00000100 | set new pin is shown on screen |
| LCD_CHANGEPIN | 0x00000200 | change pin is shown on screen |
| LCD_VERIFYPIN | 0x00000400 | verify pin is shown on screen |
| LCD_PINLOCKED | 0x00000800 | pin locked is shown on screen |
| LCD_FORMAT | 0x00001000 | format is shown on screen |
| LCD_REBOOT | 0x00002000 | reboot is shown on screen |
| LCD_SHOWBIP39 | 0x00004000 | bip39 mnemonics are show on screen |
| LCD_CHECKBIP39 | 0x00008000 | check bip39 mnemonics input is shown on screen |
| LCD_SHOWBTSSIGN | 0x00010000 | CYB sign info is shown on screen |
| LCD_PINERROR  | 0x00020000 | pin error is shown on screen |
| LCD_SELECT_MNENUM | 0x00040000 | mnemonic count selection is shown on screen  |
| LCD_SHOWM | 0x00080000 | M is shown on screen, reserved |
| LCD_SHOWTIMEOUT | 0x00100000 | timeout is shown on screen |
| LCD_SHOWEOSSIGN | 0x00200000 | eos sign info is shown on screen |
| LCD_SHOWFAIL | 0x00400000 | fail is shown on screen |
| LCD_SHOWNEOSIGN | 0x00800000 | neo sign info is show on screen |
| LCD_WAITING_TIMEOUT | 0x01000000 | waiting timeout is shown on screen |
| LCD_GET_MNENUM | 0x02000000 | getting mnemonics number is shown on screen |
| LCD_GETMNE_BYDEV | 0x04000000 | getting mnemonics is shown on screen |


#### Others definition

| Name | Value | Description |
| --- | --- | --- |
| SN_LEN | 0x20 | length of serial number |
| SESSKEY_HASH_LEN | 0x04 | length of session key hash, reserved |
| N_T_INVALID | 0xFF | N or T is invalid, reserved |

## Functions 

Before calling any methods, Make sure **WOOKONG Solo** is well connected, PIN status is [<code>PIN_LOGIN</code>](#pin-status-definition) and LCD status is [<code>LCD_NULL</code> ](#lcd-status-definition) or [<code>LCD_SHOWLOGO</code>](#lcd-status-definition), otherwise errors may be encountered.

### getDeviceInfo()

Get information of connected devices.

**Example**  
```js
const { code, result: getDeviceInfoResult} = await core.getDeviceInfo();
```

**Return format**

<code>{ code, result: [getDeviceInfoResult](#getDeviceInfoResult) }</code>


### getDeviceCount() ⇒ 
Get count of current connected devices.
Device count is returned as the value of <code>result</code> key.

**Example**  
```js
const { code, result } = await core.getDeviceCount();
```

**Return format**

<code>{ code, result}</code>

### changePIN()
Change pin of current connected device.

**Example**  
```js
const { code } = await core.changePIN();
```

**Return format**

<code>{ code }</code>

### format()
Format current connected device.

For user's convenience, this operation supports formatting **WOOKONG Solo** under [PIN_LOGOUT](#pin-status-definition) status, 

Format is a dangerous operation, all user data will be erased, make sure mnemonics were backed up already.

**Example**  
```js
const { code } = await core.format();
```

**Return format**

<code>{ code }</code>

### getAddress(coinType, derivePath, showOnScreen)

Get coin address from connected device by coin type and derive path.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| coinType | <code>Integer</code> | Must be defined in [core.constants.coins](#coreconstantscoins)  |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| showOnScreen | <code>Integer</code> | 0: not shown on screen<br/>1: shown on screen<br/>other values will be rejected |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000000, 0x80000000, 0x00000000, 0x00000000]
const { code, result: getAddressResult} = await core.getAddress(core.constants.COIN_TYPE_BTC, derivePath, 1);
```

**Return format**

<code>{ code, result: [getAddressResult](#getAddressResult) }</code>

### generateSeed(seedLen)

Generate seed in connected device, the lifecycle of device must be [LIFECYCLE_AGREE](#lifecycle-definition).
This operation require user to write down all mnemonics shown on device screen and input some of them to check.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| seedLen | <code>Integer</code> | seedLen is length of seed in bytes, a integer between [16, 32] and must be multiple of 4, see [BIP-0039](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#generating-the-mnemonic) for more details. |

**Example**  
```js
const { code } = await core.generateSeed(32);
```

**Return format**

<code>{ code }</code>

### importSeed()

Import seed into connected device, the lifecycle of device must be [LIFECYCLE_AGREE](#lifecycle-definition).
This operation require user to select mnemonics count on device screen and then input all mnemonics in order.

**Example**  
```js
const { code } = await core.importSeed();
```

**Return format**

<code>{ code }</code>

### getLibraryVersion()

Get dynamic library version.

Library version is returned in String type as value of <code>result</code> key

**Example**  
```js
const { code, result } = await core.getLibraryVersion();
```

**Return format**

<code>{ code, result: [getLibraryVersionResult](#getLibraryVersionResult) }</code>

### signBTC(derivePath, currentTX, utxos)

Sign BTC/USDT transaction.
Transaction information will show on device screen and user can press OK buton to confirm or press C buton to cancel.

**WOOKONG Solo** supports USDT omni layer which runs on BTC blockchain, so to sign a USDT transaction, just prepare the transaction data and call <code>signBTC()</code> in the same way as BTC.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| currentTX | <code>Hex String</code> | Raw transaction data in hex string format to be signed |
| utxos | <code>Array of Hex String</code> | Array of utxo in hex string format, utxo count must be identical with the input count in <code>currentTX</code> |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000000, 0x80000000, 0x00000000, 0x00000000];
const utxo1 = '0100000003e0b11a9515ee6d6b5408af881d6e4475ddbd4f4cabcffa7300fc95367fe53fd0010000006b483045022100d7e836519e2b085cae1ce9c4ee4566e14c31cf276ebc78d45b8655f84f763e5c02204fb483a7a4e5f100cbcdd223f3c21820d9e8c9f6a67f2b06bd52def46634bad901210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffffe0b11a9515ee6d6b5408af881d6e4475ddbd4f4cabcffa7300fc95367fe53fd0000000006a47304402205efa7719ce8db5454c55c21a97e89ecee20e167b848163225a30b630b2abb870022012a24df9f0c764843b8ee58a56632fc84bda23ccf7a74cade945e7c16796a42701210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffff09fb2cc0a873800b67fb143983f66d7a02a6fb7402356c64246720f31fb9eeaf010000006a473044022025dda0ab1822b2878496116b36db239aeb982760a86039fdd5c371341378763802206460f35b32a292d20473a867735068c1cff3f006eb27a15922d3b723ce92fb5401210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffff020046c323000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac1139c005000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac00000000';
const utxo2 = '0100000001dee079359248299e3f24e7877c6b1c2f361b54741f00b8056fc5001cdc750794000000006a47304402200dbbca4874b83623ea6c31970df49efbc371c120a933ea7f5ad707f7a0bc57ab02207cd31405cbcb5520e635079f1b8a8bdec9e7ea6c5aa5997ea1ee659ee4efdd7701210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffff020046c323000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac60b9eb0b000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac00000000';
const currentTX = '0100000002bf69089d98b93cd3e54fb2cc4575de550fa46b4901c8d3f59ca318fc63e002770000000000ffffffffcd6e85a4e533f56f658b80b19dee114f0bc4b0c780eb683b59221c6fe181d3570000000000ffffffff02bbb3eb0b000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac00ca9a3b000000001976a914BD2CBCF0DD693F73568F7D44C8AC26C5DAD5210088ac0000000';
const utxos = [utxo1, utxo2];
const { code, result: signBTCResult} = await signBTC(derivePath, currentTX, utxos);
```

**Return format**

<code>{ code, result: [signBTCResult](#signBTCResult) }</code>

### signLTC(derivePath, currentTX, utxos)

Sign LTC transaction.
Transaction information will show on device screen and user can press OK buton to confirm or press C buton to cancel.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| currentTX | <code>Hex String</code> | Raw transaction data in hex string format to be signed |
| utxos | <code>Array of Hex String</code> | Array of utxo in hex string format, utxo count must be identical with the input count in <code>currentTX</code> |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000002, 0x80000000, 0x00000000, 0x00000000];
const utxo1 = '0100000003e0b11a9515ee6d6b5408af881d6e4475ddbd4f4cabcffa7300fc95367fe53fd0010000006b483045022100d7e836519e2b085cae1ce9c4ee4566e14c31cf276ebc78d45b8655f84f763e5c02204fb483a7a4e5f100cbcdd223f3c21820d9e8c9f6a67f2b06bd52def46634bad901210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffffe0b11a9515ee6d6b5408af881d6e4475ddbd4f4cabcffa7300fc95367fe53fd0000000006a47304402205efa7719ce8db5454c55c21a97e89ecee20e167b848163225a30b630b2abb870022012a24df9f0c764843b8ee58a56632fc84bda23ccf7a74cade945e7c16796a42701210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffff09fb2cc0a873800b67fb143983f66d7a02a6fb7402356c64246720f31fb9eeaf010000006a473044022025dda0ab1822b2878496116b36db239aeb982760a86039fdd5c371341378763802206460f35b32a292d20473a867735068c1cff3f006eb27a15922d3b723ce92fb5401210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffff020046c323000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac1139c005000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac00000000';
const utxo2 = '0100000001dee079359248299e3f24e7877c6b1c2f361b54741f00b8056fc5001cdc750794000000006a47304402200dbbca4874b83623ea6c31970df49efbc371c120a933ea7f5ad707f7a0bc57ab02207cd31405cbcb5520e635079f1b8a8bdec9e7ea6c5aa5997ea1ee659ee4efdd7701210395e0571b441e0f2fd932906a3fd68a57098a5552dd62e22387139b1f6078223dffffffff020046c323000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac60b9eb0b000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac00000000';
const currentTX = '0100000002bf69089d98b93cd3e54fb2cc4575de550fa46b4901c8d3f59ca318fc63e002770000000000ffffffffcd6e85a4e533f56f658b80b19dee114f0bc4b0c780eb683b59221c6fe181d3570000000000ffffffff02bbb3eb0b000000001976a914cd557a2e83fb75185073a301da772885183b580c88ac00ca9a3b000000001976a914BD2CBCF0DD693F73568F7D44C8AC26C5DAD5210088ac0000000';
const utxos = [utxo1, utxo2];
const { code, result: signBTCResult} = await signLTC(derivePath, currentTX, utxos);
```

**Return format**

<code>{ code, result: [signLTCResult](#signLTCResult) }</code>

### signNEO(derivePath, currentTX, utxos)

Sign NEO transaction.
Transaction information will show on device screen and user can press OK buton to confirm or press C buton to cancel.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| currentTX | <code>Hex String</code> | Raw transaction data in hex string format to be signed |
| utxos | <code>Array of Hex String</code> | Array of utxo in hex string format, utxo count must be identical with the input count in <code>currentTX</code> |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000378, 0x80000000, 0x00000000, 0x00000000];
const utxo1 = '02000d2fead2f701f9f0ab25b4dee36f1324ab6162f2364495b8784c14a0a9393b3a370100034c38b2fcfb1929a43adc82583be8a2f8f856818fa7abaff815872dc70f73fd0000880d5d6598b2ab804a4222fd9d974becea492383ca7109885a9e3a964950e90a01002dba1a5cedf7c26122e853bf00082bc5e6b423a31d2015af364abcee082c64400000f5ddf131fe6080a6f87577c22806938e6e710f3c9869b34ad2ec1681b9e2ec900000f5ddf131fe6080a6f87577c22806938e6e710f3c9869b34ad2ec1681b9e2ec9001007f26c00a5f4e50cd0565e15c3fa515f2ba7fa88dfe8136f25ac684b9e5a640880000d13fa613284b7aa24f554e0ddb4a1d722f16bc66828261fb0fe27e0cff22899a0000626bccd65346d60d48765674ffe31d9c07611222671d15cb51c2e0d5cd710fe300008332becc8796fe73831f7eedfdfdb75b5512c9181b4fe6821319dc789df55962000048fe7161091bb7773617cb34c2034fa0a1ccd18ba9605a8f34a156ac84a1a9ab000018dec74f4267d0afc9dc9ee22cdcfa37ca855247dd258a66a63d5d3b973dcd1e0000febf4e99371568cabe370910cc1b034c9529c007036776a1b98507869eef37990000000001e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c609526000000000000c5c01ed71436525dc1a748697b3344cbd6b1a0f2014140984d589c9bd9a269182963cef0ac54cd1dbc630cb0edfc386f763ce9501e3b3f67b490228d982ae4e7576c954d51f1f76b715b6acaa141d3038e23233dd9797c2321037b0d309e6d5fa8ca2ba96b0668fbab39260d4c4e694700b93165dd54805530bbac';
const utxo2 = '0200012ace9614cfcca2bf7d0fb680b4ed22e697f386465348f5e9356fd269f587e67c0000000001e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c60d23f000000000000c5c01ed71436525dc1a748697b3344cbd6b1a0f20141403777129b9957f91e994540749045d1c07021b3e0c64e5fd71fc4399e82bb5a217c4f2f7840ee3e68602bf4dadfd357b81040de33cafcc2de31edc60300852f6c2321037b0d309e6d5fa8ca2ba96b0668fbab39260d4c4e694700b93165dd54805530bbac';
const currentTX = '800000020baa65fcf385ec1adf90a7a3249e349ccb482642113ec22471982ac9f6e8cd04000085f7a226ad5ca0a5025983c73ed556058b814e8ae8e43901eddbcb6d4bf85ec6000002e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c601027000000000000c5c01ed71436525dc1a748697b3344cbd6b1a0f2e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c60573f000000000000c5c01ed71436525dc1a748697b3344cbd6b1a0f2';
const utxos = [utxo1, utxo2];
const { code, result: signNEOResult} = await signNEO(derivePath, currentTX, utxos);
```

**Return format**

<code>{ code, result: [signNEOResult](#signNEOResult) }</code>


### signEthereum(derivePath, currentTX, isETH, erc20Info)

Sign Ethereum transaction.
This function support signing of ETH/ETC/ERC20 tokens
Transaction information will show on device screen and user can press OK buton to confirm or press C buton to cancel.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| currentTX | <code>Hex String</code> | Raw transaction data in hex string format to be signed |
| isETH | <code>bool</code> | When signing ETH or ERC20 tokens on ETH, this must be <code>true</code>, When signing ETC or ERC20 tokens on ETC, this must be <code>false</code> |
| erc20Info | <code>object</code> | Contains 2 keys: <code>name</code>  and  <code>decimal</code>. <br/> **MUST** be ignored if intented to sign ETH/ETC.|
| erc20Info.name | <code>String</code> | Name of the ERC20 token |
| erc20Info.decimal | <code>Integer</code> | Decimal of the ERC20 token |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x8000003c, 0x80000000, 0x00000000, 0x00000000];
const currentTX = 'f8698084b2d05e008301d4c094859a9c0b44cb7066d956a958b0b82e54c9e44b4b80b844a9059cbb000000000000000000000000f03232ebb232786aff2dab33a6badc173a1656ab0000000000000000000000000000000000000000000000001d24b2dfac520000018080';
const erc20Info = { name: "iETH", decimal: 18 };
const { code, result: signEthereumResult} = await signEthereum(derivePath, currentTX, true, erc20Info);
```

**Return format**

<code>{ code, result: [signEthereumResult](#signEthereumResult) }</code>

### signCYB(derivePath, currentTX)

Sign CYB transaction.
Transaction information will show on device screen and user can press OK buton to confirm or press C buton to cancel.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> |  |
| currentTX | <code>Hex String</code> | Raw transaction data in hex string format to be signed |

**Example**  
```js
const derivePath = [0, 0, 1, 0x80];
const currentTX = '26e9bf2206a1d15c7e5b0100e8030000000000000080af0280af020a00000000000000000001040a7a68616e6773793133330343594203435942050500';
const { code, result: signCYBResult} = await signCYB(derivePath, currentTX);
```

**Return format**

<code>{ code, result: [signCYBResult](#signCYBResult) }</code>

### signEOS(derivePath, currentTX)

Sign EOS transaction.
Transaction information will show on device screen and user can press OK buton to confirm or press C buton to cancel.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| currentTX | <code>Hex String</code> | Raw transaction data in hex string format to be signed |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x800000c2, 0x80000000, 0x00000000, 0x00000000];
const currentTX = '740970d9ff01b504632fede1adc3dfe55990415e4fde01e1b8f315f8136f476c14c2675b01245f705dd7000000000100a6823403ea3055000000572d3ccdcd012029c2ca557a735700000000a8ed3232212029c2ca557a735790558c8677954c3c102700000000000004454f530000000000000000000000000000000000000000000000000000000000000000000000000000';
const { code, result: signEOSResult} = await signEOS(derivePath, currentTX);
```

**Return format**

<code>{ code, result: [signEOSResult](#signEOSResult) }</code>

### signXRP(derivePath, currentTX)

Sign XRP transaction.
Transaction information will show on device screen and user can press OK buton to confirm or press C buton to cancel.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| currentTX | <code>Hex String</code> | Raw transaction data in hex string format to be signed |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000090, 0x80000000, 0x00000000];
const currentTX = '53545800120000228000000024000967036140000000000186A068400000000000000A732102AFCCB4B29A86D50EF367BE689BBC6DE679D35EE54BD05D963FBCF1156BCC7F858114EF531520EBC1BA8958559F77483318BA8501560C8314C64A6FB05B2A2CDBC6852E0EC3FAA437CFA3B76D';
const { code, result: signXRPResult} = await signXRP(derivePath, currentTX);
```

**Return format**

<code>{ code, result: [signXRPResult](#signXRPResult) }</code>

### getPubKey(derivePath, coinType)

Get coin public key from conencted device.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| coinType | <code>Integer</code> | Must be defined in [core.constants.coins](#coreconstantscoins)  |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000090, 0x80000000, 0x00000000];
const { code, result: getPubKeyResult} = await getPubKey(derivePath, constants.coins.COIN_TYPE_XRP);
```

**Return format**

<code>{ code, result: [getPubKeyResult](#getPubKeyResult) }</code>

### clearCOS()

Clear user part of firmware for update.
Should be used together with [<code>updateCOS</code>](#updatecos)

**Return format**

<code>{ code }</code>


### updateCOS(cosData, callback)

Update user part of firmware.

[<code>clearCOS()</code>](#clearcos) **MUST** be called befor this operation.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| cosData | <code>Array of byte</code> | Firmware data bytes |
| callback | <code>(progress: Number) => void</code> | Update progress callback  |


**Return format**

<code>{ code }</code>

### verifyFileSignature()

reserved


## Function result objects

### getDeviceInfoResult

**Properties**

| Name | Type | Description |
| --- | --- | --- |
| ucPINState | <code>Integer</code> | [PIN state](#pin-status-definition) |
| ucCOSType | <code>Integer</code> | [Firmware type](#firmware-type-definition) |
| ucChainType | <code>Integer</code> | [Chain type](#chain-type-definition) |
| pbSerialNumber | <code>String</code> | Device serial number |
| pbCOSVersion | <code>Array</code> | Firmware version |
| ucLifeCycle | <code>Integer</code> | [Lifecycle](#lifecycle-definition) |
| nLcdState | <code>Integer</code> | [LCD State](#lcd-status-definition) |
| pbSessKeyHash | <code>Array</code> | Reserved |
| nN | <code>Integer</code> | Reserved |
| nT | <code>Integer</code> | Reserved |
| pbBLEVersion | <code>Array</code> | Reserved |


**Example**  
```js
{
    "ucPINState": 1,
    "ucCOSType": 1,
    "ucChainType": 1,
    "pbSerialNumber": "2019031800003",
    "pbCOSVersion": [ 1, 1, 0, 28 ],
    "ucLifeCycle": 2,
    "nLcdState": 0,
    "pbSessKeyHash": [ 0, 0, 0, 0 ],
    "nN": 0,
    "nT": 0,
    "pbBLEVersion": [ 0, 0, 0, 0 ]
}
```

### getDeviceCountResult

**Properties**

| Name | Type | Description |
| --- | --- | --- |
| ucPINState | <code>Integer</code> | [PIN state](#pin-status-definition) |
| ucCOSType | <code>Integer</code> | [Firmware type](#firmware-type-definition) |
| ucChainType | <code>Integer</code> | [Chain type](#chain-type-definition) |
| pbSerialNumber | <code>String</code> | Device serial number |
| pbCOSVersion | <code>Array</code> | Firmware version |
| ucLifeCycle | <code>Integer</code> | [Lifecycle](#lifecycle-definition) |
| nLcdState | <code>Integer</code> | [LCD State](#lcd-status-definition) |
| pbSessKeyHash | <code>Array</code> | Reserved |
| nN | <code>Integer</code> | Reserved |
| nT | <code>Integer</code> | Reserved |
| pbBLEVersion | <code>Array</code> | Reserved |


**Example**  
```js
{
    ucPINState: 1,
    ucCOSType: 1,
    ucChainType: 1,
    pbSerialNumber: '2019031800003',
    pbCOSVersion: [ 1, 1, 0, 28 ],
    ucLifeCycle: 2,
    nLcdState: 0,
    pbSessKeyHash: [ 0, 0, 0, 0 ],
    nN: 0,
    nT: 0,
    pbBLEVersion: [ 0, 0, 0, 0 ]
}
```

### getAddressResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| address | <code>String</code> |  |

**Example**  
```js
{
    address: '1LMuCezVR5i1bURqzv1C6BJKEiC2SG52Lq'
}
```

### signBTCResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| strSigns | <code>Array of String</code> | Signatures in hex string format |

**Example**  
```js
{
    strSigns: [
        "483045022100f2dc7f9c3d7ff71677e0a1198827d41a57f33b40dc7b722f58a2fbaf613a6b67022015586301a2f4a8b84b370cc144dc0fa3ae13a3c85d330bf9196bdbf3b6bec0dc0121035c638c7c849914150b1d373de4c743fae588fba21e82d9d5539c323370f63312",
        "483045022100b8e9dce6206a3270e0454097b0921e2019ecb55f38882825a36fa1c0da4cbb00022001f932f471e072cebc696a18b3e7afd2f5d569edcebcb4695fa5591c9e699cb20121035c638c7c849914150b1d373de4c743fae588fba21e82d9d5539c323370f63312"
    ]
}
```

### signLTCResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| strSigns | <code>Array of String</code> | Signatures in hex string format |

**Example**  
```js
{
    strSigns: [
        "483045022100d71075a2253bac220b42a77c3521aefba8c58ea683eeeaf1b0da9edfa5da772802206f7a9a6a97bc0fec8b770d819b4de91c54c1303729e5a2daacc8c78516b48186012103a275008038546b3df838777edce6f24169de10fc466e412400df56e225bb0981",
        "48304502210096a9a9b2b9305d2bda48ef529c83a65482d7521b50f959b64d9209fa56843a74022041b6f0cc8a9d2505536e65564e9d4ff382ca41450e588dedb9c9bdedae4d02ed012103a275008038546b3df838777edce6f24169de10fc466e412400df56e225bb0981"
    ]
}
```

### signNEOResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| signs: | <code>object</code> |  |
| signs.invocation | <code>String</code> | Invocation of signature in hex string format |
| signs.verification | <code>String</code> | Verification of signature in hex string format |

**Example**  
```js
{
	signs: {
		invocation: '40a588e8b4a39af2b22db52ac00c0dbf7eab8a14bc3e38c2de1d5d33d7ca3f85ab1fb6f3ff9ecf52a56759147102a7a339dea643008eef9a574bc8ddddd4cc814e',
		verification: '21027e7a4a8f6faca492f65fd1729c8e222725880e539ce3411ff8c611a4af5338cfac'
	}
}
```

### signEthereumResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| sign: | <code>object</code> |  |
| sign.raw | <code>String</code> | Raw signature in hex string format |
| sign.r | <code>String</code> | r value of raw signature in hex string format |
| sign.s | <code>String</code> | s value of raw signature in hex string format |
| sign.v | <code>String</code> | v value of raw signature in hex string format |

**Example**  
```js
{
	signs: {
		raw: '6214506908c8159f1aaa6730ed4649aae07ba1db72a9d9eca5e432cd2e61fd376d780ab4cde28e0ad1cd22232f821f0a429de4ca946131c6925a9c0699e5f8ad01',
        r: '0x6214506908c8159f1aaa6730ed4649aae07ba1db72a9d9eca5e432cd2e61fd37',
        s: '0x6d780ab4cde28e0ad1cd22232f821f0a429de4ca946131c6925a9c0699e5f8ad',
        v: '0x01'
	}
}
```

### signCYBResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| signature: | <code>String</code> | Signature in hex string format |

**Example**  
```js
{
	signature: '200dbd4ed68095f621b120bde110601b0f264bbdef49f5a688a8b78b10adfaab0236ac6851e2ac63eb1d2e4a10b87ca81365ec4622694625f118e8455158dc1fbf'
}
```

### signEOSResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| signature: | <code>String</code> | Signature in hex string format |

**Example**  
```js
{
	signature: 'SIG_K1_KdMWfc8NFi3xvWTdk4bxtGMUWbpFcs7FCnNAXiXjkfUAsfKfAb6ZxTUnzFqoL1F3cEMNMrxm8RBp7Ctp1kkUq41ftxCGUX'
}
```

### signXRPResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| sign: | <code>String</code> | Signature in hex string format |

**Example**  
```js
{
	sign: '3045022100a1b2b64ba34278c58a87a041bad00d02bcd10664e1a6c931e807fb8dbeee6f2602201a7f112b1012ef0755fd4d9429503f6c5bce24e59180cac1d44aa9d266eb3727'
}
```

### getPubKeyResult

**Properties**
| Name | Type | Description |
| --- | --- | --- |
| pubKey: | <code>String</code> | Public key in hex string format |

**Example**  
```js
{
	pubKey: '03576b0d3a7bf961ad0a81d76b98380d319aa0d8195b01f817569b4238da506f04'
}
```

## Firmware update procedure
 
The whole firmware update procedure may be divided into two steps:
1. Erase current existing user firmware by calling [<code>clearCOS()</code>](#clearCOS)
   
2. Make sure user firmware of connected **WOOKONG Solo** device had been erased successfully, then call [<code>updateCOS(cosData, callback)</code>](#updatecoscosdata-callback)

Notice: [<code>clearCOS()</code>](#clearCOS) and [<code>updateCOS(cosData, callback)</code>](#updatecoscosdata-callback) may result device communication fail on some version of OS, e.g: macOS High Sierra (10.13), so when you got a code that is not equal to [<code>DEV_COMMAND_INVALID</code>](#coreconstantsrets) returned by getDeviceInfo(), you should try to disconnect and reconnect **WOOKONG Solo**.


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