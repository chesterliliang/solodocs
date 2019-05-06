# Functions 

Before calling any methods, Make sure **WOOKONG Solo** is well connected, PIN status is [<code>PIN_LOGIN</code>](./3-core.constants.md#pin-status-definition) and LCD status is [<code>LCD_NULL</code> ](./3-core.constants.md#lcd-status-definition) or [<code>LCD_SHOWLOGO</code>](./3-core.constants.md#lcd-status-definition), otherwise errors may be encountered.

- [Functions](#functions)
  - [getDeviceInfo()](#getdeviceinfo)
  - [getDeviceCount()](#getdevicecount)
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

## getDeviceInfo()

Get information of connected devices.

**Example**  
```js
const { code, result: getDeviceInfoResult} = await core.getDeviceInfo();
```

**Return format**

<code>{ code, result: [getDeviceInfoResult](./5-Function-result-objects.md#getDeviceInfoResult) }</code>


## getDeviceCount()
Get count of current connected devices.
Device count is returned as the value of <code>result</code> key.

**Example**  
```js
const { code, result } = await core.getDeviceCount();
```

**Return format**

<code>{ code, result}</code>

## changePIN()
Change pin of current connected device.

**Example**  
```js
const { code } = await core.changePIN();
```

**Return format**

<code>{ code }</code>

## format()
Format current connected device.

For user's convenience, this operation supports formatting **WOOKONG Solo** under [PIN_LOGOUT](./3-core.constants.md#pin-status-definition) status, 

Format is a dangerous operation, all user data will be erased, make sure mnemonics were backed up already.

**Example**  
```js
const { code } = await core.format();
```

**Return format**

<code>{ code }</code>

## getAddress(coinType, derivePath, showOnScreen)

Get coin address from connected device by coin type and derive path.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| coinType | <code>Integer</code> | Must be defined in [core.constants.coins](./3-core.constants.md#coreconstantscoins)  |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| showOnScreen | <code>Integer</code> | 0: not shown on screen<br/>1: shown on screen<br/>other values will be rejected |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000000, 0x80000000, 0x00000000, 0x00000000]
const { code, result: getAddressResult} = await core.getAddress(core.constants.COIN_TYPE_BTC, derivePath, 1);
```

**Return format**

<code>{ code, result: [getAddressResult](./5-Function-result-objects.md#getAddressResult) }</code>

## generateSeed(seedLen)

Generate seed in connected device, the lifecycle of device must be [LIFECYCLE_AGREE](./3-core.constants.md#lifecycle-definition).
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

## importSeed()

Import seed into connected device, the lifecycle of device must be [LIFECYCLE_AGREE](./3-core.constants.md#lifecycle-definition).
This operation require user to select mnemonics count on device screen and then input all mnemonics in order.

**Example**  
```js
const { code } = await core.importSeed();
```

**Return format**

<code>{ code }</code>

## getLibraryVersion()

Get dynamic library version.

Library version is returned in String type as value of <code>result</code> key

**Example**  
```js
const { code, result } = await core.getLibraryVersion();
```

**Return format**

<code>{ code, result: [getLibraryVersionResult](./5-Function-result-objects.md#getLibraryVersionResult) }</code>

## signBTC(derivePath, currentTX, utxos)

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

<code>{ code, result: [signBTCResult](./5-Function-result-objects.md#signBTCResult) }</code>

## signLTC(derivePath, currentTX, utxos)

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

<code>{ code, result: [signLTCResult](./5-Function-result-objects.md#signLTCResult) }</code>

## signNEO(derivePath, currentTX, utxos)

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

<code>{ code, result: [signNEOResult](./5-Function-result-objects.md#signNEOResult) }</code>


## signEthereum(derivePath, currentTX, isETH, erc20Info)

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

<code>{ code, result: [signEthereumResult](./5-Function-result-objects.md#signEthereumResult) }</code>

## signCYB(derivePath, currentTX)

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

<code>{ code, result: [signCYBResult](./5-Function-result-objects.md#signCYBResult) }</code>

## signEOS(derivePath, currentTX)

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

<code>{ code, result: [signEOSResult](./5-Function-result-objects.md#signEOSResult) }</code>

## signXRP(derivePath, currentTX)

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

<code>{ code, result: [signXRPResult](./5-Function-result-objects.md#signXRPResult) }</code>

## getPubKey(derivePath, coinType)

Get coin public key from conencted device.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| derivePath | <code>Array of Integer</code> | Following [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) is strongly recommended |
| coinType | <code>Integer</code> | Must be defined in [core.constants.coins](./3-core.constants.md#coreconstantscoins)  |

**Example**  
```js
const derivePath = [0, 0x8000002c, 0x80000090, 0x80000000, 0x00000000];
const { code, result: getPubKeyResult} = await getPubKey(derivePath, constants.coins.COIN_TYPE_XRP);
```

**Return format**

<code>{ code, result: [getPubKeyResult](./5-Function-result-objects.md#getPubKeyResult) }</code>

## clearCOS()

Clear user part of firmware for update.
Should be used together with [<code>updateCOS</code>](#updatecos)

**Return format**

<code>{ code }</code>


## updateCOS(cosData, callback)

Update user part of firmware.

[<code>clearCOS()</code>](#clearcos) **MUST** be called befor this operation.

**Parameters**

| Param | Type | Description |
| --- | --- | --- |
| cosData | <code>Array of byte</code> | Firmware data bytes |
| callback | <code>(progress: Number) => void</code> | Update progress callback  |


**Return format**

<code>{ code }</code>

## verifyFileSignature()

reserved