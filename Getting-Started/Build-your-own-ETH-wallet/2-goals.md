# Define the features

We are going to build a simple cli(command line interface) ETH wallet with several basic commands as shown below, for parsing convenience, all parameters should be seprated with one space(` `), and spaces must not been seen in parameters' values. In this whole tutorial, we will not check the validities of the inputted parameters and assume them are all valid and correct.

Usage of the commands are written with reference to [docopt](http://docopt.org/).

1. info
   
   This command is used to get device info, and it does not need any other parameters.

   **Usage**  
   
   ```shell
   info
   ```


   **Example**  
   
   ```shell
   info
   ```

2. init
   
   This command is used to generate a seed inside **WOOKONG Solo**, it needs one parameter to identify whether to generate a seed by **WOOKONG Solo** itself randomly, or by the user-inputted mnemonics. Seed_len must be present when generate a seed by **WOOKONG Solo** itself randomly, it is length of seed in bytes, a integer between [16, 32] and must be multiple of 4, see [BIP-0039](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#generating-the-mnemonic) for more details. 

   **Usage**  
   
   ```shell
   init (generate <seed_len>)|import
   ```

   **Example**  
   
   ```shell
   init generate 32
   ```

   or

   ```shell
   init import
   ```

3. format
   
   This command is used to remove all user-related data in **WOOKONG Solo**, including clear seed stored inside, clear PIN and set its state to unset, reset lifecycle to [LIFECYCLE_AGREE](../../API/3-core.constants.md#clifecycle-definition). 

   **Usage**  
   
   ```shell
   format
   ```

   **Example**  
   
   ```shell
   format
   ```

4. addr
   
   This command is used to get ETH address, and it needs only one parameter for derive path, address should be shown on device screen.

   **Usage**  
   
   ```shell
   addr <derive_path>
   ```
   
   **Example**  
   
   ```shell
   addr [0,2147483692,2147483708,2147483648,0,0]
   ```

5. Get balance
   
   This command is used to get ETH balance on chain, and it needs only one parameter for derive path.

   **Usage**  
   
   ```shell
   balance <derive_path>
   ```
   
   **Example**  
   
   ```shell
   balance [0,2147483692,2147483708,2147483648,0,0]
   ```

6. Send ETH to other addresses
   
   This command is used to transfer ETH, and it needs 3 parameters for derive path, recipient address and transfer value.

   **Usage**  
   
   ```shell
   send (<derive_path> <to> <value>)
   ```
   
   **Example**  
   
   ```shell
   send [0,2147483692,2147483708,2147483648,0,0] 0x7F825230F5F2A26523999c98e0E3f7E2697085A9 0.0001
   ```
