# Data-Encryption-Standard-ns-assignment-
#This project offers a simple yet powerful Python implementation of the Data Encryption Standard (DES)
from Crypto.Cipher import DES
import binascii

def pad(text):
    """ Pad text to ensure it's a multiple of 8 bytes """
    while len(text) % 8 != 0:
        text += ' '
    return text

def des_encrypt(key, text):
    """ Encrypt the text using DES """
    des = DES.new(key, DES.MODE_ECB)
    padded_text = pad(text)
    encrypted_text = des.encrypt(padded_text.encode())
    return binascii.hexlify(encrypted_text).decode()

def des_decrypt(key, encrypted_hex_text):
    """ Decrypt hex-encoded text using DES """
    des = DES.new(key, DES.MODE_ECB)
    encrypted_text = binascii.unhexlify(encrypted_hex_text)
    decrypted_text = des.decrypt(encrypted_text).decode().rstrip()
    return decrypted_text

# Improved dynamic user interaction with validation
if __name__ == "__main__":
    while True:
        action = input("Do you want to (E)ncrypt or (D)ecrypt? ").strip().upper()
        if action in ["E", "D"]:
            break  # Valid input, exit loop
        else:
            print("Invalid choice! Please enter 'E' for encryption or 'D' for decryption.")

    while True:
        key = input("Enter an 8-character key: ").encode()
        if len(key) == 8:
            break  # Valid key, exit loop
        else:
            print("Error: Key must be exactly 8 bytes long!")

    if action == "E":
        plaintext = input("Enter text to encrypt: ")
        encrypted = des_encrypt(key, plaintext)
        print(f"Encrypted (Hex): {encrypted}")

    elif action == "D":
        encrypted_hex_text = input("Enter hex-encoded text to decrypt: ")
        decrypted = des_decrypt(key, encrypted_hex_text)
        print(f"Decrypted: {decrypted}")
