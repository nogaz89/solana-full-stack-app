## The Complete Guide to Full Stack Solana Development with React, Anchor, Rust, and Phantom

Code examples to go with the blog post available [here](https://dev.to/dabit3/the-complete-guide-to-full-stack-solana-development-with-react-anchor-rust-and-phantom-3291)

![Header image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nl0h25rp5h9ytg5wnrj7.png)

### Prerequisites

1. Node.js - I recommend installing Node using either [nvm](https://github.com/nvm-sh/nvm) or [fnm](https://github.com/Schniz/fnm)

2. Solana Tool Suite - You can see the installation instructions [here](https://docs.solana.com/cli/install-solana-cli-tools). _note - I had a very hard time getting everything working on an M1 Mac, mainly `solana-test-validator` and `cargo-build-bpf`. I finally figured it out, and posted my solution [here](https://github.com/project-serum/anchor/issues/95#issuecomment-913090162). I'm sure at some point this will be fixed and work out of the box._

3. Anchor - Anchor installation was pretty straight-forward for me. You can find the installation instructions [here](https://project-serum.github.io/anchor/getting-started/installation.html).

4. Solana browser wallet - I recommend [Phantom](https://phantom.app/), which is what I have tested this app with.

### To build

1. Clone the repo

```sh
git clone git@github.com:dabit3/complete-guide-to-full-stack-solana.git
```

2. Change into the project directory you'd like to run

3. Install the dependencies

```sh
yarn
```

4. Build the anchor project

```sh
anchor build
```

5. Fetch the project ID for the build:

```sh
solana address -k target/deploy/mysolanaapp-keypair.json
```

6. Update the project ID in the Rust program in lib.rs:

```rust
// mysolanaapp/src/lib.rs
declare_id!("your-program-id");
```

and in Anchor.toml:

```toml
# Anchor.toml
[programs.localnet]
mysolanaapp = "your-program-id"
```

7. Run the tests

```sh
anchor test
```

8. Start a local Solana node

```sh
solana-test-validator
```

9. Fund your wallet

```sh
solana airdrop 1000 <your Solana address>
```

10. Deploy contract

```sh
anchor deploy
```

11. Copy IDL in the Application using the copy script

```sh
node copyIdl.js
```

12. Change into the **app** directory and install the dependencies:

```sh
cd app && npm install
```

13. Run the client-side app

```sh
npm start
```