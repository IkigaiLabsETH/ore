# ORE

**ORE is a cross-border digital currency everyone can mine.**


## API
- [`Consts`](api/src/consts.rs) – Program constants.
- [`Error`](api/src/error.rs) – Custom program errors.
- [`Event`](api/src/error.rs) – Custom program events.
- [`Instruction`](api/src/instruction.rs) – Declared instructions and arguments.

## Instructions
- [`Claim`](program/src/claim.rs) – Distributes ORE from the treasury to a miner.
- [`Close`](program/src/close.rs) – Closes a proof account returns the rent to the owner.
- [`Open`](program/src/open.rs) – Opens a new proof account for a miner.
- [`Mine`](program/src/mine.rs) – Verifies a hash and increments a miner's claimable balance.
- [`Stake`](program/src/stake.rs) – Stakes ORE with a miner to increase their multiplier.
- [`Reset`](program/src/reset.rs) – Resets the program for a new epoch.
- [`Update`](program/src/update.rs) – Updates a proof account's miner authority.
- [`Upgrade`](program/src/upgrade.rs) – Migrates ORE v1 tokens to ORE v2, one-for-one.
- [`Initialize`](program/src/initialize.rs) – Initializes the program and creates the global accounts.

## State
 - [`Bus`](api/src/state/bus.rs) - An account (8 total) which tracks and limits the amount ORE mined each epoch.
 - [`Config`](api/src/state/config.rs) – A singleton account which manages program-wide variables.
 - [`Proof`](api/src/state/proof.rs) - An account (1 per user) which tracks a miner's current hash and current stake.
 - [`Treasury`](api/src/state/treasury.rs) – A singleton account which has authority to mint ORE and holds onto user stake.


## Tests

To run the test suite, use the Solana toolchain: 

```
cargo test-sbf
```

For line coverage, use llvm-cov:

```
cargo llvm-cov
```
## Fork

Yes, forking the Ore smart contract to deploy your own token is possible. Here's a detailed guide on the steps you would need to follow to achieve this:

### Steps to Fork and Deploy Your Own Token:

1. **Understand the Existing Contract:**
   - Review the Ore smart contract code thoroughly to understand its functionality, dependencies, and configuration. Look for aspects such as mining logic, reward distribution, and interaction with the Solana blockchain.
   - Identify any external libraries or dependencies used in the Ore contract.

2. **Set Up Development Environment:**
   - Install necessary development tools for Solana smart contract development. This typically includes Rust (for writing smart contracts), Solana CLI, and a local testnet environment for testing.
   - Set up a local development environment using tools like Anchor, a framework for Solana smart contract development.

3. **Clone the Ore Repository:**
   - If the Ore contract is open-source, clone the repository to your local machine. If it is not open-source, you may need to recreate the functionality based on available documentation and reverse engineering.
   ```sh
   git clone <repository-url>
   cd <repository-directory>
   ```

4. **Modify the Contract:**
   - Rename the token and update any branding or token-specific parameters in the contract code.
   - Adjust the mining logic, reward distribution, and any other customizable aspects to fit your specific requirements.
   - Ensure that the emission rate, computational challenge, and reward mechanisms are correctly implemented for your new token.

5. **Deploy the Contract:**
   - Compile the modified contract using the Solana CLI and Anchor.
   ```sh
   anchor build
   ```
   - Deploy the smart contract to the Solana testnet for initial testing.
   ```sh
   solana program deploy <compiled-program-file>
   ```

6. **Test Thoroughly:**
   - Test the deployed contract on the Solana testnet to ensure it functions as expected. Verify that mining works, rewards are distributed correctly, and there are no security vulnerabilities.
   - Conduct extensive testing with different scenarios and edge cases to ensure robustness.

7. **Audit the Contract:**
   - Before deploying to the mainnet, consider having the contract audited by a reputable blockchain security firm. This will help identify and fix potential security issues.
   - Ensure compliance with any regulatory requirements that may apply to your token and its use case.

8. **Deploy to Mainnet:**
   - Once testing is complete and the contract is audited, deploy the smart contract to the Solana mainnet.
   ```sh
   solana program deploy <compiled-program-file> --url mainnet-beta
   ```

9. **Launch and Promote:**
   - Announce the launch of your new token and provide detailed documentation on how users can participate in mining and use the token.
   - Engage with the community and provide support for any issues or questions that arise.

### Key Considerations:

- **Scalability:** Ensure that the deployed contract can handle high transaction volumes, especially if your token becomes popular.
- **Security:** Regularly update and maintain the contract to address any discovered vulnerabilities or exploits.
- **Community Engagement:** Build a strong community around your token to drive adoption and participation in mining.

### Example Structure for Your Token Fork:

#### Contract Initialization:
```rust
#[program]
mod my_token {
    use super::*;
    pub fn initialize(ctx: Context<Initialize>, ...params...) -> ProgramResult {
        // Initialization logic
    }
}
```

#### Mining Logic:
```rust
#[program]
mod my_token {
    use super::*;
    pub fn mine(ctx: Context<Mine>, ...params...) -> ProgramResult {
        // Mining logic and proof-of-work verification
    }
}
```

#### Reward Distribution:
```rust
#[program]
mod my_token {
    use super::*;
    pub fn distribute_rewards(ctx: Context<DistributeRewards>, ...params...) -> ProgramResult {
        // Reward distribution logic
    }
}
```

### Final Thoughts

By forking the Ore smart contract and deploying your own token, you can leverage existing innovations while customizing the solution to meet your specific needs. 


## Step-by-Step Troubleshooting and Fixes:

1. **Ensure Anchor is Installed Correctly:**
   - Verify that Anchor is installed by running:
     ```sh
     anchor --version
     ```
   - If it’s not installed, follow the installation steps:
     ```sh
     cargo install --git https://github.com/project-serum/anchor --tag v0.20.1 anchor-cli --locked
     ```

2. **Check Rust Installation:**
   - Make sure Rust is installed and updated:
     ```sh
     rustup update
     rustup default stable
     ```

3. **Verify Solana CLI Installation:**
   - Ensure Solana CLI is installed and set up properly:
     ```sh
     solana --version
     ```
   - If not installed, follow the installation steps:
     ```sh
     sh -c "$(curl -sSfL https://release.solana.com/v1.10.32/install)"
     ```

4. **Project Configuration:**
   - Ensure you are in the root directory of your Anchor project.
   - Check your `Anchor.toml` file for correct configuration.

5. **Build Dependencies:**
   - Make sure all dependencies are correctly set up. Run:
     ```sh
     anchor build
     ```
   - If there are errors, they may indicate missing dependencies or incorrect configurations. Follow the error messages for clues.

### Common Issues and Fixes:

#### Issue: Missing Dependencies or Incorrect Configuration
- **Fix:**
  - Ensure your `Cargo.toml` is correctly configured with all dependencies.
  - Ensure `Anchor.toml` has the correct program ID and configurations.

#### Issue: Environment Variables
- **Fix:**
  - Set up the necessary environment variables:
    ```sh
    export ANCHOR_WALLET=~/.config/solana/id.json
    export ANCHOR_PROVIDER_URL=https://api.devnet.solana.com
    ```

#### Issue: Rust Version Compatibility
- **Fix:**
  - Sometimes, specific versions of Rust are required. Switch to a compatible version:
    ```sh
    rustup install nightly
    rustup default nightly
    ```

### Detailed Example of Configuration Files:

#### Cargo.toml
```toml
[package]
name = "my_token"
version = "0.1.0"
edition = "2018"

[dependencies]
anchor-lang = "0.20.1"
anchor-spl = "0.20.1"

[features]
default = ["client"]

[workspace]
members = ["programs/*"]
```

#### Anchor.toml
```toml
[programs.localnet]
my_token = "3rdYvFyz3SxxVxT5G4obJZ9g7gG8A8hJvMnJ6JGVV4Ws"

[provider]
cluster = "localnet"
wallet = "~/.config/solana/id.json"

[scripts]
test = "cargo test-bpf"
```

### Example Command Sequence:

1. **Clone Repository:**
   ```sh
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Install Anchor and Dependencies:**
   ```sh
   cargo install --git https://github.com/project-serum/anchor --tag v0.20.1 anchor-cli --locked
   rustup update
   rustup default stable
   ```

3. **Set Environment Variables:**
   ```sh
   export ANCHOR_WALLET=~/.config/solana/id.json
   export ANCHOR_PROVIDER_URL=https://api.devnet.solana.com
   ```

4. **Build Project:**
   ```sh
   anchor build
   ```

5. **Deploy to Testnet:**
   ```sh
   anchor deploy
   ```

### Good Luck

If after these steps the `anchor build` command still doesn’t work, consider providing the exact error messages for more specific troubleshooting. You might also want to consult the [Anchor documentation](https://project-serum.github.io/anchor/getting-started/introduction.html) or reach out to the Anchor community for further assistance.

