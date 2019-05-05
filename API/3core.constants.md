# core.constants

core.constants is collection of constants may be used in fuctions as parameters or return

## core.constants.rets
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

## core.constants.coins

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

## core.constants.lengths

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

## core.constants.devinfo

### PIN status definition

| Name | Value | Description |
| --- | --- | --- |
| PIN_INVALID_STATE | 0xFF | PIN in a invalid state |
| PIN_LOGOUT | 0x00 | PIN status is logged out |
| PIN_LOGIN | 0x01 | PIN status is logged in |
| PIN_LOCKED | 0x02 | PIN is locked |
| PIN_UNSET | 0x03 | PIN is unset, should set pin first |

### Chain type definition

| Name | Value | Description |
| --- | --- | --- |
| CHAIN_TYPE_FORMAL | 0x01 | chain type of device is formal net |
| CHAIN_TYPE_TEST | 0x02 | chain type of device is test net |

### Firmware version length definition

| Name | Value | Description |
| --- | --- | --- |
| COS_VERSION_LEN | 0x04 | length of firmware version |
| BLE_VERSION_LEN | 0x04 | length of ble version |

### Firmware type definition

| Name | Value | Description |
| --- | --- | --- |
| COS_TYPE_INDEX | 0x01 | reserved  |
| COS_TYPE_INVALID | 0xFF | firmware type is invalid |
| COS_TYPE_DRAGONBALL | 0x00 | firmware type is **WOOKONG Enterprise** |
| COS_TYPE_PERSONAL | 0x01 | firmware type is **WOOKONG Solo** |
| COS_TYPE_BIO | 0x02 | firmware type is **WOOKONG Bio** |

### Lifecycle definition

| Name | Value | Description |
| --- | --- | --- |
| LIFECYCLE_INVALID | 0xFF | lifecycle is invalid |
| LIFECYCLE_AGREE | 0x01 | seed not generated |
| LIFECYCLE_USER | 0x02 | normal state, seed generated |
| LIFECYCLE_PRODUCE | 0x04 | producting state, reserved |

### LCD status definition

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


### Others definition

| Name | Value | Description |
| --- | --- | --- |
| SN_LEN | 0x20 | length of serial number |
| SESSKEY_HASH_LEN | 0x04 | length of session key hash, reserved |
| N_T_INVALID | 0xFF | N or T is invalid, reserved |