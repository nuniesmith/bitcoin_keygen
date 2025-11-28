# Bitcoin Key Generator

A simple, secure Rust application for generating BIP39 seed phrases for Bitcoin hardware wallets (Coldcard, Trezor, Ledger, etc.). Designed to run on air-gapped computers for maximum security.

## Features

- Generates 24-word BIP39 mnemonic seed phrases (256 bits of entropy)
- Creates printable output optimized for metal plate punching/storage
- Calculates master key fingerprint for hardware wallet verification
- Outputs multiple file formats for different use cases
- Designed for air-gapped systems (no network dependencies during execution)

## Requirements

- Rust (latest stable version)
- Air-gapped computer (recommended)
- Printer for generating physical backup

## Installation

```bash
cargo build --release
```

The compiled binary will be in `target/release/bitcoin-keygen`.

## Development

### Running Tests

```bash
cargo test
```

The test suite includes:
- Mnemonic generation validation
- Seed derivation consistency
- Master key derivation
- Fingerprint format validation
- Output file generation
- File format verification

### Building Documentation

```bash
cargo doc --open
```

Documentation is automatically generated and published to GitHub Pages on each push to the main branch.

### Code Quality

The project uses:
- `cargo fmt` for code formatting
- `cargo clippy` for linting
- GitHub Actions for continuous integration

## CI/CD

This project uses GitHub Actions for:
- **Testing**: Runs test suite on every push and pull request
- **Code Quality**: Checks formatting and runs clippy
- **Documentation**: Generates and publishes docs to GitHub Pages
- **Example Output**: Generates example output files as artifacts

## Usage

### Basic Usage

```bash
./target/release/bitcoin-keygen
```

This will generate a new seed phrase with the default label "Bitcoin Wallet".

### Custom Label

```bash
./target/release/bitcoin-keygen "My Wallet Name"
```

### Output Files

The application creates an `output/` directory with the following files:

1. **`seed_phrase_printable.txt`** - Main printable file optimized for metal plate punching
   - Includes all 24 words in numbered format
   - Multiple layout options (4-column grid and single column)
   - Security warnings and verification checklist
   - Hardware wallet import instructions
   - Master key fingerprint for verification

2. **`seed_words_simple.txt`** - Simple numbered list of words
   - Easy to read and verify
   - Minimal formatting

3. **`seed_words_for_coldcard.txt`** - One word per line
   - Optimized for manual entry into hardware wallets
   - No numbers or formatting

## Security Best Practices

1. **Run on Air-Gapped Computer**: Execute this application only on a computer that has never been and will never be connected to the internet.

2. **Print and Verify**: 
   - Print the `seed_phrase_printable.txt` file
   - Manually verify all 24 words are correct
   - Double-check the fingerprint

3. **Metal Plate Storage**:
   - Use the printed file as a template for punching your metal plate
   - Store the metal plate in a secure, fireproof location
   - Create a backup copy in a separate geographic location

4. **Clean Up**:
   - Delete all generated files from the computer after printing
   - Securely wipe the computer's storage if possible
   - Never store seed phrases on internet-connected devices

5. **Test First**:
   - Import the seed into your hardware wallet
   - Verify the fingerprint matches
   - Test with a small transaction before storing large amounts

## Hardware Wallet Import Process

The generated seed phrase is compatible with all BIP39-compatible hardware wallets including Coldcard, Trezor, Ledger, and others.

### Example: Coldcard
1. Power on your Coldcard device
2. Navigate to: `Advanced > Danger Zone > Seed Functions > Import Existing`
3. Select `24 words` when prompted
4. Enter the 24 words in order (1-24)
5. Verify the fingerprint matches the one shown in the output
6. Set a secure PIN code
7. Test with a small transaction

### Example: Trezor
1. Connect your Trezor device
2. Follow the setup wizard
3. Select "Recover wallet" and choose "24 words"
4. Enter the 24 words in order
5. Verify the fingerprint matches
6. Set a passphrase (optional)
7. Test with a small transaction

### Example: Ledger
1. Connect your Ledger device
2. Open the Bitcoin app
3. Follow the recovery process
4. Enter the 24 words when prompted
5. Verify the fingerprint matches
6. Set a PIN code
7. Test with a small transaction

## Technical Details

- **Mnemonic Standard**: BIP39
- **Word Count**: 24 words (256 bits entropy)
- **Network**: Bitcoin Mainnet
- **Key Derivation**: BIP32 (master key derivation)
- **Fingerprint Format**: 8-character hex (hardware wallet compatible)

## Dependencies

- `bitcoin` - Bitcoin protocol implementation
- `bip39` - BIP39 mnemonic generation
- `rand` / `getrandom` - Cryptographically secure random number generation
- `chrono` - Timestamp generation

## License

This software is provided as-is for personal use. Use at your own risk.

## Disclaimer

**CRITICAL SECURITY WARNING**: 

- This seed phrase provides full access to your Bitcoin wallet
- Anyone with access to your seed phrase can steal your funds
- Store backups securely and never share your seed phrase
- Test recovery procedures before storing significant amounts
- The authors are not responsible for any loss of funds

