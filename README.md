# 🚀 Bitcoin Mnemonic Sweeper with Sound Notifications 🎉

Welcome to the Bitcoin Mnemonic Sweeper project! This script generates BIP-39 mnemonic phrases, converts them to private keys, and attempts to sweep any funds found to a designated address. If a sweep is successful, it plays a cheerful sound notification. 🎶

📖 Introduction
This project is designed to help you find and sweep Bitcoin funds from generated mnemonic phrases. The script runs indefinitely, generating new mnemonics, checking for associated Bitcoin balances, and sweeping any funds found to your specified address. It even plays a sound to notify you of successful sweeps! 🎵

## ✨ Features
- 🔄 **Indefinite Mnemonic Generation**: Continuously generates BIP-39 12-word mnemonic phrases.
- 🔑 **Private Key Conversion**: Converts mnemonics to Bitcoin private keys.
- 💰 **Fund Sweeping**: Checks for Bitcoin balances and sweeps any found funds to your designated address.
- 🔔 **Sound Notifications**: Plays a sound when a sweep is successful.

## 🛠️ Getting Started

### Prerequisites
Before you begin, ensure you have met the following requirements:
- You are using a Windows machine.
- You have Python 3.x installed.
- You have an internet connection.

### Installation
1. **Clone the Repository**
   ```sh
   git clone https://github.com/tianrich/bipscraper.git
   cd bipscraper
   ```

2. **Install Required Packages**
   Use the following `pip` command to install all necessary dependencies:
   ```sh
   pip install bitcoin bit mnemonic
   ```

3. **Run the Script**
   ```sh
   python sweep.py
   ```

## 🚀 Usage
To use the Bitcoin Mnemonic Sweeper, simply run the script. The script will continuously generate mnemonic phrases, convert them to private keys, check for balances, and sweep any found funds to your specified address. If a sweep is successful, you'll hear a sound notification.

## 📝 Detailed Explanation

### Generating Mnemonics
The script uses the `mnemonic` library to generate BIP-39 12-word mnemonic phrases. These phrases are generated indefinitely in a loop.

### Converting to Private Keys
Each mnemonic phrase is converted to a SHA-256 hashed private key. This key is then encoded into Wallet Import Format (WIF) for compatibility with Bitcoin wallets.

### Sweeping Funds
Using the `bit` library, the script checks for any Bitcoin balance associated with the generated private key. If a balance is found, it attempts to send the funds to the designated sweep address.

### Sound Notifications
The `winsound` library is used to play a default Windows sound when a sweep is successful. This auditory notification helps you quickly identify successful sweeps.

## 🤝 Contributing
Contributions are welcome! Here's how you can contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-foo`).
3. Make your changes.
4. Commit your changes (`git commit -m 'Add feature foo'`).
5. Push to the branch (`git push origin feature-foo`).
6. Open a pull request.

## 📜 License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## 🌟 Show Your Support
If you like this project, please give it a ⭐ on GitHub! Donations welcome: 3FxQzNxA1MYEjmtQjEYfKisLPYq1b7hBCf

--- 

Thanks for checking out the Bitcoin Mnemonic Sweeper project! We hope you find it useful and fun. If you have any questions or suggestions, feel free to open an issue or contribute to the project. Happy sweeping! 🧹💸  Donations welcome: 3FxQzNxA1MYEjmtQjEYfKisLPYq1b7hBCf
