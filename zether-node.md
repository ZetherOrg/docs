# Running a Zether Node

This guide will walk you through the steps to run a Zether node. Follow each step carefully to initialize, start, and run your node properly.

## Steps to Run a Zether Node

### Step 1: Create a Folder and Download the Files

1. Create a new folder where you want to store your Zether node files.
2. Download the binary file and the genesis file (`zether.json`) and place them in this folder.

### Step 2: Initialize the Genesis and Define Directory

1. Use the following command to initialize the genesis block and specify the data directory:

    ```bash
    ./geth --datadir data init zether.json
    ```

   This command initializes the data folder (`data`) using the genesis file (`zether.json`).

### Step 3: Start the Node in Fullsync Mode

1. Start your node using the `geth` command. When running your node for the first time, add the `console` flag to interact with it:

    ```bash
    ./geth --datadir ./data --networkid 715131 --http --http.addr 0.0.0.0 --http.port 8545 --http.api personal,eth,net,web3,miner --http.corsdomain "*" --syncmode "full" console
    ```

   This command will start your node in full synchronization mode and enable an interactive console.

### Step 4: Add Peers to Sync

1. To start syncing with the network, add peers using the `admin.addPeer` command:

    ```javascript
    admin.addPeer("enode://a96143d21ac86019f3dc375d618f2ffa7d45541bc783ccb718427750982068af372c64c947730b6ae088f24fc1100364a34e5cb19218e7abf2ffc686bf461cef@209.74.72.123:30157")
    
    admin.addPeer("enode://ebcd7217534f82a97e455a9fb8f31c9da112c33375995a767881164801c6ad2dd7bd0488da2c5881aa5a766d727d9327fe8b52ba1567047c7295b3242564770a@209.74.72.124:30157")
    ```

   Adding these peers helps to connect your node with the network for synchronization.

### Step 5: Running or Restarting the Node

1. After adding peers, you can keep the node running or restart it without the `console` flag.
2. If you want to enable mining, you can add the `--mine` flag along with mining parameters:

    ```bash
    ./geth --datadir ./data --networkid 715131 --http --http.addr 0.0.0.0 --http.port 8545 --http.api personal,eth,net,web3,miner --http.corsdomain "*" --syncmode "full" --mine --miner.threads=1 --miner.etherbase 0xYourEthereumAddress
    ```

   Replace `0xYourEthereumAddress` with your own Ethereum address to receive mining rewards.

## Additional Information

- **API Exposure**: The `--http.api` flag exposes specific APIs. Adjust the options depending on your needs.
- **Security Considerations**: Ensure that your node is protected, especially when running in an open network, by configuring the firewall and using appropriate HTTP settings.

## Troubleshooting

- **Genesis File Error**: Ensure the genesis file path is correct during initialization.
- **Connection Issues**: Make sure your firewall is allowing the necessary ports for peer-to-peer connections.

Happy node running! If you run into issues, feel free to open an issue in the repository.

