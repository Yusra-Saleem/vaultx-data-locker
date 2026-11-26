# VaultX Secure Data Locker

> Zero-knowledge encrypted cloud data locker implementing client-side AES-256-GCM cryptography, role-gated access control, and audit logs.

## 1. System Overview

VaultX is a confidential data vault engineered to provide zero-knowledge protection for sensitive files and enterprise records. All encryption operations occur client-side prior to storage ingestion, ensuring that neither the server nor storage administrators possess the cryptographic keys required to decrypt user data.

## 2. Technical Architecture

```
[ User Plaintext File ]
        │
        ▼
[ Client-Side PBKDF2 Key Derivation ] ── (Master Passphrase + Salt)
        │
        ▼
[ AES-256-GCM Encryption Engine ] ── (Generates Ciphertext + Auth Tag)
        │
        ▼
[ Vault Storage Ingestion ] ── (Zero Knowledge Stored on Server)
```

### Cryptographic Specifications
- **Cipher Algorithm:** AES-256-GCM (Authenticated Encryption with Associated Data)
- **Key Derivation Function:** PBKDF2 with SHA-256 (100,000+ iterations)
- **Integrity Verification:** 128-bit authentication tag verification on decryption
- **Platform Runtime:** Python 3.10+, Streamlit, Cryptography library

## 3. Key Security Features

- **True Zero-Knowledge:** Plaintext never touches disk unencrypted; decryption keys are transient and held only in client session memory.
- **Tamper-Evident Integrity:** GCM authentication tags detect any bit-level modification or unauthorized ciphertext corruption.
- **Role-Based Access Control:** Role-gated metadata mapping and user access policies.
- **Automated Test Suite:** Comprehensive test coverage validating encryption rounds, key derivation determinism, and corrupted ciphertext rejection.

## 4. Directory Structure

```
vaultx-data-locker/
├── src/                      # Cryptographic core modules and vault logic
│   ├── crypto_engine.py      # AES-256-GCM implementation
│   ├── auth_manager.py       # Role-gated authorization logic
│   └── app.py                # Interactive Streamlit vault interface
├── tests/                    # Cryptographic test suites and validation tests
├── requirements.txt          # Python dependencies
└── user_data.json            # Encrypted vault registry
```

## 5. Getting Started

```bash
git clone https://github.com/Yusra-Saleem/vaultx-data-locker.git
cd vaultx-data-locker

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

pip install -r requirements.txt
streamlit run src/app.py
```

## 6. Author and License

- **Author:** Yusra Saleem
- **Portfolio:** [yusrasaleem.dev](https://yusrasaleem.dev)
- **License:** Licensed under the [MIT License](LICENSE).
