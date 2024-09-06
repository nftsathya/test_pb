# **Steps to Create Multiple Web3 Accounts from Seed Phrase**

**1. Install Python and Required Libraries**
First, you’ll need Python and the web3.py and eth-account libraries installed.

# Update package list
     sudo apt-get update

# Install Python 3 and pip
     sudo apt-get install python3 python3-pip -y

# Install the required libraries
     pip3 install web3 eth-account mnemonic


**2. Create a Python Script to Derive Accounts from a Seed Phrase**

 1.Open a terminal and create a Python script file:

     nano create_wallets_from_seed.py

 2.Add the following Python code to derive multiple accounts from the seed phrase and save them to a text file:

     from eth_account.hdaccount import Mnemonic
     from eth_account import Account
     import os
     
     # Enable the HD wallet features in eth-account
     Account.enable_unaudited_hdwallet_features()
     
     # Function to derive an Ethereum account from a seed phrase and a derivation path
     def derive_account_from_mnemonic(mnemonic_phrase, index):
         # Derivation path for Ethereum based on BIP44 standard (m/44'/60'/0'/0/index)
         derivation_path = f"m/44'/60'/0'/0/{index}"
     
         # Generate the account from the mnemonic phrase and derivation path
         account = Account.from_mnemonic(mnemonic_phrase, account_path=derivation_path)
     
         return account.address, account.key.hex()
     
     # Function to generate multiple accounts from a seed phrase and save them to a file
     def create_multiple_accounts_from_seed(seed_phrase, num_accounts, output_file):
         with open(output_file, 'w') as f:
             for i in range(num_accounts):
                 address, private_key = derive_account_from_mnemonic(seed_phrase, i)
                 f.write(f"Address: {address}, Private Key: {private_key}\n")
                 print(f"Generated Wallet {i + 1}: {address}")
         print(f"\n{num_accounts} wallets generated and saved to {output_file}")
     
     if __name__ == "__main__":
         # Your seed phrase (mnemonic)
         mnemonic_phrase = "your twelve or twenty-four word seed phrase here"
     
         # Number of accounts to generate
         num_of_accounts = 10  # You can change this number
     
         # Output file to save generated accounts
         output_file = "wallets_from_seed.txt"
     
         # Create the accounts from the seed phrase
         create_multiple_accounts_from_seed(mnemonic_phrase, num_of_accounts, output_file)

**3. Ensure you have the required dependencies installed by below command and allow you to generate Ethereum addresses from your seed phrase.**

     pip3 install web3 eth-account mnemonic


**4. Update the Script with Your Seed Phrase**

 Replace the mnemonic_phrase value with your actual 12 or 24-word seed phrase. It should look something like this:

     mnemonic_phrase = "your twelve or twenty-four word seed phrase here"

 Example (don't use this phrase; it's insecure):
   
     mnemonic_phrase = "buddy improve tenant ozone soccer penalty flower broom tape sunset swarm disease"

**5. Run the Script**

 To generate multiple accounts based on your seed phrase, run the Python script:

     python3 create_wallets_from_seed.py

This script will generate Ethereum wallet addresses and private keys based on the BIP-44 standard (m/44'/60'/0'/0/ derivation path) and store them in a file named wallets_from_seed.txt.


**6. View the Generated Accounts**

After running the script, the accounts (addresses and private keys) will be stored in the wallets_from_seed.txt file. You can view them by running:

     cat wallets_from_seed.txt

It will output something like this:
     
     address: 0xAbc123..., Private Key: 0xYourPrivateKey1Address: 0xDef456..., Private Key: 0xYourPrivateKey2Address: 0x789Ghi..., Private Key: 0xYourPrivateKey3

Each address corresponds to a unique Ethereum account derived from the seed phrase, using a different derivation index (e.g., /0/0, /0/1, /0/2, etc.).

**7. Security Considerations**

**Seed Phrase Security:**
   
Be very careful with your seed phrase and private keys. They give full control over the corresponding Ethereum accounts. Ensure the generated file and your seed phrase are kept secure.

**File Permissions:**
        
Restrict access to the private key file to make it accessible only by the owner:
        
     chmod 600 wallets_from_seed.txt

* This limits access to the file, ensuring only the user has read and write permissions.

**8. Customize the Script**

**Number of Accounts:** Change the num_of_accounts variable in the script to create as many accounts as you need.
     
**Derivation Path:** The script uses the standard Ethereum derivation path m/44'/60'/0'/0/index. If you need to use a different path, adjust the derivation_path in the script.
    
By following these steps, you can create multiple Ethereum accounts from an existing seed phrase and store the addresses and private keys in a text file on your Linux system.
