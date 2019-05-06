# Function result objects

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

## getDeviceInfoResult

**Properties**

| Name | Type | Description |
| --- | --- | --- |
| ucPINState | <code>Integer</code> | [PIN state](./3-core.constants.md#pin-status-definition) |
| ucCOSType | <code>Integer</code> | [Firmware type](./3-core.constants.md#firmware-type-definition) |
| ucChainType | <code>Integer</code> | [Chain type](./3-core.constants.md#chain-type-definition) |
| pbSerialNumber | <code>String</code> | Device serial number |
| pbCOSVersion | <code>Array</code> | Firmware version |
| ucLifeCycle | <code>Integer</code> | [Lifecycle](./3-core.constants.md#lifecycle-definition) |
| nLcdState | <code>Integer</code> | [LCD State](./3-core.constants.md#lcd-status-definition) |
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

## getDeviceCountResult

**Properties**

| Name | Type | Description |
| --- | --- | --- |
| ucPINState | <code>Integer</code> | [PIN state](./3-core.constants.md#pin-status-definition) |
| ucCOSType | <code>Integer</code> | [Firmware type](./3-core.constants.md#firmware-type-definition) |
| ucChainType | <code>Integer</code> | [Chain type](./3-core.constants.md#chain-type-definition) |
| pbSerialNumber | <code>String</code> | Device serial number |
| pbCOSVersion | <code>Array</code> | Firmware version |
| ucLifeCycle | <code>Integer</code> | [Lifecycle](./3-core.constants.md#lifecycle-definition) |
| nLcdState | <code>Integer</code> | [LCD State](./3-core.constants.md#lcd-status-definition) |
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

## getAddressResult

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

## signBTCResult

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

## signLTCResult

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

## signNEOResult

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

## signEthereumResult

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

## signCYBResult

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

## signEOSResult

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

## signXRPResult

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

## getPubKeyResult

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