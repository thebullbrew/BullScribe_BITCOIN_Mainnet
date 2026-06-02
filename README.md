# BullScribe_BITCOIN_Mainnet

PROLOGUE:
  On Bitcoin's mainnet I'm going to use the most common insscription method through Ordinals (inscriptions). 
  I will use Bitcoin Core + ord, the real Bitcoin mainnet Ordinals setup.
  I can “inscribe” data — image, text, HTML, metadata, etc. onto an individual satoshi, the smallest unit of BTC. 
  Ordinals give satoshis individual identities, and inscriptions attach content to them, creating Bitcoin-native digital artifacts. 
  It does not require a sidechain or separate token, and the content is stored on-chain through Bitcoin transactions.

You need:

  1. A Bitcoin wallet that supports Ordinals, such as Xverse, UniSat, Leather, Magic Eden wallet, etc.
  2. BTC for transaction fees.
  3. Your NFT image/content.
  4. An inscription service or your own Ordinals node.
  5. A Bitcoin address that supports receiving Ordinals.

WARNING: it is usually more expensive and slower than minting on Solana.
Bitcoin block space is limited, so larger files cost more.
For NFT projects, Ethereum or Solana are better for learning and building a web app. 
Bitcoin Ordinals are better if you want the “this is permanently inscribed on Bitcoin mainnet” flex. 


# Step 1 | Install Bitcoin Core

Note: You are not deploying a contract. You are using your own Bitcoin node and the ord CLI to inscribe a file into a Bitcoin transaction.

On Mac, easiest with Homebrew:
brew install bitcoin

Check it:

bitcoind --version
bitcoin-cli --version


# Step 2 | Create your Bitcoin config

Create the config folder if needed:

mkdir -p ~/Library/Application\ Support/Bitcoin
nano ~/Library/Application\ Support/Bitcoin/bitcoin.conf

Add:

INI

server=1
txindex=1
rpcuser=joao
rpcpassword=CHANGE_THIS_TO_A_LONG_RANDOM_PASSWORD


Save it.

ord needs Bitcoin Core with the transaction index enabled. 
The official Ordinals wallet guide specifically says Bitcoin Core needs txindex=1.  



# Step 3 | Start Bitcoin Core

bitcoind -daemon


Check sync status:
bitcoin-cli getblockchaininfo

Look for:
"initialblockdownload": false

If it says true, your node is still syncing.

This is the painful part: Bitcoin mainnet sync can take a long time and a lot of disk space. You generally need the full chain indexed before using ord properly.


# Step 4 | Install ord
