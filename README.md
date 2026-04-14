# Stream Cipher with Custom PRNG

Author: Drei Abmab

## Overview
This project demonstrates a custom implementation of a **stream cipher** using a **pseudorandom number generator (PRNG)**. It showcases how encryption and decryption work using XOR operations, along with a more secure approach to key generation using **nonce-based seed derivation** and **SHA-256 hashing**.

---

## Objectives
- Implement a custom PRNG for keystream generation  
- Demonstrate XOR-based encryption and decryption  
- Show deterministic behavior of seeded PRNGs  
- Improve security using nonce + secret-based seed derivation  
- Simulate real-world stream cipher concepts  

---

## How It Works

### 1. Custom PRNG (`crand`)
- Uses a combination of:
  - Linear Congruential Generator (LCG)
  - Lagged Fibonacci-style sequence
- Deterministic: same seed → same keystream
- Generates a continuous stream of pseudorandom numbers

---

### 2. Encryption Process
1. Convert plaintext to hexadecimal  
2. Generate keystream using PRNG  
3. Combine PRNG outputs into a hex key  
4. XOR plaintext with keystream  
5. Output ciphertext (hex)

```python
cipher = plaintext ⊕ keystream
```

---

### 3. Decryption Process
Regenerate the same keystream using the same seed
XOR ciphertext with keystream
Recover original plaintext

```python
plaintext = ciphertext ⊕ keystream
```

---

### 4. Seed Derivation (Improved Security)
- Combines:
    - Nonce (unique per message)
    - Shared Secret
- Uses SHA-256 hashing:

```python
seed = SHA256(nonce || secret) mod 2^32
```
- Prevents keystream reuse → critical for stream cipher security

---

### 5. Secure Message Format
```python
[ nonce | ciphertext ]
```
- Receiver:
    1. Extracts nonce
    2. Recomputes seed
    3. Regenerates keystream
    4. Decrypts message

--- 

## Example Output
#### Encryption
```python
Plaintext: Hello Cryptography
Cipher (hex): c93f7df7e2fc1b246255ca2ebc3f1fb20b9a
```
#### Decryption
```python
Recovered Plaintext: Hello Cryptography
```
#### Secure Decryption with Derived Seed
```python
Derived seed: 42847799
Plaintext: this is a message.
```

# Security Notes
- This is a learning implementation, not production-ready
- Custom PRNGs are not cryptographically secure
- XOR encryption is only secure if:
    - Keystream is truly random
    - Keystream is never reused
- Using nonce + hashing improves security but does not replace standard cryptographic algorithms





