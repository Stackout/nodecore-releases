This is intended as a self-contained readme.txt to be alongside the binary downloads. It is on the public wiki: https://wiki.veriblock.org/index.php?title=NodeCore_Readme

__TOC__

# Overview 

General links:
* Public wiki for documentation: https://wiki.veriblock.org
* Block Explorer for TestNet: https://TestNet.Explore.Veriblock.org
* Submit any technical issues to github: https://github.com/VeriBlock
* Home page: https://www.veriblock.org

VeriBlock Proof-of-Proof has 4 components:
* nodecore-*-rc.*.zip - Backend NodeCore instance. 
* nodecore-reference-pow.zip - Proof-of-Work miner to add next nodecore block
* nodecore-pop-*-rc.*.zip - Proof-of-Proof mining
* nodecore-cli-*-rc.*.zip - Command Line. Use this to send transactions.

First step is to run a local instance of NodeCore. Whether you mine or use the command line, you'll need a local instance running. For example the command line connects to your local instance, and that local instance connects to the entire network.

# Get each part running 

## Prerequisites 

* Java v1.8
* Bitcoin Core (TestNet) - If doing PoP Mining TestNet

## How to run NodeCore 

# Unzip the zip file
# In the bin folder, Add the "nodecore.properties" file as a sibling of nodecore.bat. This will specify your local IP, and the peers that you connect to.
# In the bin folder, run either nodecore (for linux) or nodecore.bat (for windows)

<pre>
peer.publish.address=<your_public_IP>
peer.external.hosts=94.130.33.180\:6500,78.46.106.162\:6500
</pre>

When you first run NodeCore, it will create several other log files in the bin folder, and load the existing blockchain.

## How to run the Command Line 

# Ensure that nodecore is running (see previous step)
# Unzip VeriBlock.NodeCore.Cli-0.2.0.zip
# In the bin folder, run either VeriBlock.NodeCore.Cli (for linux) or VeriBlock.NodeCore.Cli.bat (for windows)
# Connect to the local instance by running this command "connect 127.0.0.1:10500"
# Type "help" to see all available commands. You should see a list of many commands, such as "getinfo"
# Run "getinfo". You should see data back such as

<pre>
rpc (127.0.0.1:10500) > {
  "payload": {
    "default_address": {
      "address": "V6RRxmzJAhLkeWTzcFzQkQEgP2hC1e",
      "amount": 0
    },
    "estimated_hash_rate": 56232,
    "number_of_blocks": 104,
    "transaction_fee": 1,
    "last_block": {
      "pow_coinbase_reward": 35000000000,
      "pop_coinbase_reward": 0,
      "transaction_fees": 1,
      "size": 62,
      "number": 103,
      "timestamp": 1520466056,
      "hash": "000000F4FCE491047796B5EFBEAE482787FF948152D11CB7",
      "previous_hash": "0000006FC1D6387C3DEDFD2B4EB9DEC788621F53705797BB",
      "difficulty": 51331648,
      "winning_nonce": 762757820,
      "ledger_hash": "FAF249E56914265BFCF5D02850F41AE086CE0D9FF89531B0"
    },
    "difficulty": 1000000
  },
  "success": true,
  "messages": [}
</pre>

## How to run the PoW Miner 

The PoW Miner helps get the next block added to the VeriBlock blockchain. It will connect to a local instance of NodeCore, using UCP on port 8501.

# Ensure that nodecore is running
# In the Command Line, run the "startpool". This will start the UCP NodeCore protocol on port 8501, which the miner needs.
# Unzip nodecore-reference-pow.tar
# In the bin folder, run either nodecore-reference-pow (for linux) or nodecore-reference-pow.bat (for windows)
# Enter the input arguments
## How many threads would you like to mine on? --> such as 2 or 8.
## What host:port would you like to connect to for mining? --> 127.0.0.1:8501
## What address would you like to mine to? --> the default address for your local instance of nodecore, such as "V6RRxmzJAhLkeWTzcFzQkQEgP2hC1e". Run getinfo in the commandline to see the default address.

## How to run the PoP Miner 

'''Prerequisites:'''

See this Bitcoin page for background info: https://en.bitcoin.it/wiki/Running_Bitcoin

# Download Bitcoin Core (https://bitcoin.org/en/download), and catch up on testnet. This may take a while depending on your network connection.
# Run bitcoin TestNet by passing in the parameter. 
## bitcoin-qt.exe -testnet
# Set up a rpc user and password in the bitcoin.conf file
## In Bitcoin Core, goto: Settings > Options > Main (tab) > Open Config File (button).
## If prompted with "The configuration file is used to...", then click ok.
## bitcoin.conf (a plaintext file) will open.
## specify the flags like below (server=1, rpcuser=your_username, rpcpassword=your_password), and save the file. Re-click the "Open Config File" to ensure the settings did indeed save (they should have)

<pre>
server=1
rpcuser=bitcoinrpc
rpcpassword=someTestNetPassword123
</pre>

# Get an address from unspent
## Goto: Help > Debug Window > Console Tab
## Enter the command "listunspent"
## You will get a JSON result. Pull the value of an address, such as "mwAY47kNhN2TY1nc23Y18aDi4botjpGzAy"

<pre>
  {
    "txid": "7111e775e553e44657f650d9a400981455707715ec1c4bf6bc376881a75f7d22",
    "vout": 1,
    "address": "mwAY47kNhN2TY1nc23Y18aDi4botjpGzAy",
    "account": "",
    "scriptPubKey": "76a914aba57562278e5d543e33a20e5ae1b8427b51ad0988ac",
    "amount": 0.33900000,
    "confirmations": 65,
    "spendable": true,
    "solvable": true,
    "safe": true
  }, 
</pre>

Get Bitcoin on the testnet from a faucet. Running PoP requires a small amount of Bitcoin. We do not want to endorse a specific faucet, but you can see a list here: https://en.bitcoin.it/wiki/Testnet#Faucets


'''Run the PoP Miner'''

# Run a local instance of NodeCore
# Unzip nodecore-pop-*.tar
# In the bin folder, run either nodecore-pop (for linux) or nodecore-pop.bat (for windows)
# You will be prompted for a series of questions. Below is sample inputs. Note that TestNet port is 18332 (not 18333).

<pre>
Please enter the VeriBlock NodeCore host [Default: 127.0.0.1](]):
 > 127.0.0.1
Please enter the VeriBlock NodeCore port [10500](Default:):
 > 10500
Please enter the Bitcoin RPC host [127.0.0.1](Default:):
 > 127.0.0.1
Please enter the Bitcoin RPC port [8332](Default:):
 > 18332
Please enter a funded Bitcoin address you would like to use for PoP:
 > mwAY47kNhN2TY1nc23Y18aDi4botjpGzAy
Please enter your Bitcoin RPC username:
 > bitcoinrpc
Please enter your Bitcoin RPC password:
 > someTestNetPassword123
How many BTC would you like to pay as a transaction fee for each PoP? (Suggested: 0.001)
 > 0.001
</pre>

Note that after entering this info once, it will be saved to a ncpop.properties file for future reference.

Because PoP Mining costs a small amount of BTC, you will be prompted for each transaction with something like: "Press enter to pay 0.001 BTC to perform a PoP! (q to quit)"

If the PoP Miner appears frozen, hit "ENTER" to proceed.

Go back to your Bitcoin Core, Transactions tab, and you will see PoP Transactions. Drill down on a transaction and you'll see a transaction ID. After a few minutes, this transaction ID should show up on testnet blockexplorers, such as http://testnet.coinsecrets.org.

<pre>
Status: 0/unconfirmed, in memory pool
Date: 3/9/2018 14:33
Debit: 0.00000000 BTC
Transaction fee: -0.00100000 BTC
Net amount: -0.00100000 BTC
Transaction ID: 52bac8bad5c9d71f1adcf166c5ef5e651f269851b1816b61cb99ed62268f512b
Transaction total size: 283 bytes
Output index: 0
</pre>

Drill down on the block explorer, and you will see the proof in the OP_RETURN. Ignore the first 4 characters, look at the last 160 (80 bytes), and that is your proof on the BTC testnet!

<pre>
OP_RETURN
4c5000000001000000f29717032fb910956d001e9ae5554540864b4c998cf7233ca3ff78109365086b0e7ad55c480ce9dd55fa6763275aa2eedc0319ca1c0ed60f1df7918c1b4232bfdc584dfdbaa50ae224
</pre>

# Common Use Cases 

## Send transactions across the network  

Using the Command Line, you can send transactions from one address to another.

# Open the Command Line and connect it to a local instance of NodeCore
# run the send command, targeting an address to send TO (the command will be smart enough to pick an address that has sufficient funds) 
# run: send 1000 VE2TkS4er4JeZJRnPkSKUdSeaAew5E
# It will take several minutes for the transaction to get approved by PoW miners and propagated across the network to other nodecore instances
# in the meantime, run these command lines to see that transaction: 
## getpendingtransactions
## gethistory
# Check the transaction on the website: https://testnet.explore.veriblock.org

Running gethistory will show a snippet like:
<pre>
        {
          "type": "signed",
          "signed": {
            "signature": "3045022100E6CD7E006A99D357402D2811979C5DC1511BB343ECA1895C2B3D27F43360C49A022005D1012C8180D509E4B69B6BB5E1BB89050128355A8F03AC77A4CCFD1D7795D4",
            "public_key": "3056301006072A8648CE3D020106052B8104000A034200040AFCD379B9F1880B22A9444301716BBB677335920198BCE4894F2AF9D96C963661C101608541FC337C2E1FD941D39126AC2709902AB647B150C236D456721D13",
            "signature_index": 2,
            "transaction": {
              "size": 56,
              "txid": "5D2BC42D4FD25EB17F64E00BE51B718449B7B0FE844541855E35D5136B5F1F8C",
              "data": "",
              "type": "standard",
              "fee": 1,
              "timestamp": 0,
              "source_amount": 2334,
              "merkle_path": "",
              "source_address": "V89fUr16YU6zmAGfr1wVN3Gwa7bgcy",
              "bitcoin_transaction": "",
              "bitcoin_block_header_of_proof": "",
              "endorsed_block_header": "",
              "context_bitcoin_block_headers": [              "outputs": [
                {
                  "address": "V7ePN8RRX4ULYuGdec7QWnQbqDx6gQ",
                  "amount": 2333
                }
              ](],)
            }
          }
        }
</pre>

## Add new blocks to the blockchain (Proof-of-Work Mining) 

# Run the PoW Miner per instructions above (start local nodecore, open the command line, run startpool, etc...)
# You are mining! As users submit transactions, you'll help add those transactions to the next block

## Secure to Bitcoin (Proof-of-Proof Mining) 

# Run the PoP Miner per instructions above
# You are PoP Mining!

# How to see what's happening 

## Command Line 

The command line uses the public API from NodeCore. A complete reference listing is on the public wiki: https://wiki.veriblock.org/index.php?title=NodeCore_CommandLine

Some of the especially useful commands are:

help: Provides a list of all the commands. Run "help <command>" for more details.

getbalance: Returns the balance for a given address (or all addresses if none is specified)

getinfo: Returns general information about this node and the presently-known blockchain

getpeerinfo: Returns a list of connected peers

startpool: Starts the built-in pool service in NodeCore

## VeriBlock Explorer website 

The VeriBlock explorer shows the block and transaction details on the VeriBlock blockchain. If you make a transaction, it should show up here.

https://testnet.explore.veriblock.org

## Bitcoin Explorer 

The BTC testnet explorer shows the block and transaction details for BTC testnet. When running Proof-of-Proof transactions, the proof will show up in the OP_RETURN code on Bitcoin (i.e. VeriBlock secures to Bitcoin)

Here is one such testnet explorer:

http://testnet.coinsecrets.org/

# FAQ 

## Where do I get coins to test with? 

* Run the PoW Miner and get block rewards
* TODO - Send a message to the public community channel, and someone can send you test coins --> TODO, which exact channel?

# Troubleshooting 

## PoW Miner won't start 

Ensure that you run startpool on NodeCore (using the Command Line)

Ensure that you have a local instance of NodeCore already running

## PoP Miner appears frozen 

The PoP Miner is interactive. A PoP transaction requires a small amount of BTC, so before paying it prompts you to hit "ENTER". The system may appear frozen until you hit ENTER to pay the next transaction.

## Commandline getinfo returns error 

Ensure that the connected NodeCore instance is fully caught up, else it will return an error like:

<pre>
rpc (127.0.0.1:10500) > ERROR: [V800] Remote service call failure io.grpc.StatusRuntimeException: UNAVAILABLE
</pre>

## One of the apps is frozen 

If this is windows, clicking on the console scrollbar may free the application. Hit enter to continue running.
