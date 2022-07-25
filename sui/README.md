<p align="center">
  <img height="100" height="auto" src="https://user-images.githubusercontent.com/50621007/174559198-c1f612e5-bba2-4817-95a8-8a3c3659a2aa.png">
</p>

# Sui node setup for devnet

Official documentation:
- Official manual: https://github.com/MystenLabs/sui/blob/main/doc/src/build/fullnode.md
- Experiment with Sui DevNet: https://docs.sui.io/explore/devnet
- Check you node health: https://node.sui.zvalid.com/

## Minimum hardware requirements
- CPU: 2 CPU
- Memory: 4 GB RAM
- Disk: 50 GB SSD Storage

## Recommended hardware requirements
- CPU: 2 CPU
- Memory: 8 GB RAM
- Disk: 50 GB SSD Storage

> Storage requirements will vary based on various factors (age of the chain, transaction rate, etc) although we don't anticipate running a fullnode on devnet will require more than 50 GBs today given it is reset upon each release roughly every two weeks.

## (OPTIONAL) Installation takes more than 10 minutes, so we recommend to run in a screen session
To create new screen session named `sui`
```
screen -S sui
```

To attach to existing `sui` screen session
```
screen -Rd sui
```

## Set up your Sui full node
### Option 1 (automatic)
You can setup your Sui full node in minutes by using automated script below
```
wget -O sui.sh https://raw.githubusercontent.com/nodesxploit/testnet/main/sui/sui.sh && chmod +x sui.sh && ./sui.sh
```

### Option 2 (manual)
You can follow [manual guide](https://github.com/nodesxploit/testnet/blob/main/sui/manual_install.md) if you better prefer setting up node manually

## Check status of your node
```
curl -s -X POST http://127.0.0.1:9000 -H 'Content-Type: application/json' -d '{ "jsonrpc":"2.0", "method":"rpc.discover","id":1}' | jq .result.info
```

You should see something similar in the output:
```json
{
  "title": "Sui JSON-RPC",
  "description": "Sui JSON-RPC API for interaction with the Sui network gateway.",
  "contact": {
    "name": "Mysten Labs",
    "url": "https://mystenlabs.com",
    "email": "build@mystenlabs.com"
  },
  "license": {
    "name": "Apache-2.0",
    "url": "https://raw.githubusercontent.com/MystenLabs/sui/main/LICENSE"
  },
  "version": "0.1.0"
}
```

## Post installation
After setting up your Sui node you have to register it in the [Sui Discord](https://discord.gg/b5vWu33f):
1) navigate to `#📋node-ip-application` channel
2) post your node endpoint url
```
http://<YOUR_NODE_IP>:9000/
```

## Check your node health status
Enter your node IP into https://node.sui.zvalid.com/

Healthy node should look like this:

![image](https://user-images.githubusercontent.com/50621007/175829451-a36d32ff-f30f-4030-8875-7ffa4e999a24.png)

## Update Sui Fullnode version
```
wget -qO update.sh https://raw.githubusercontent.com/nodesxploit/testnet/main/sui/tools/update.sh && chmod +x update.sh && ./update.sh
```

## (OPTIONAL) Update configs
```
wget -qO update_configs.sh https://raw.githubusercontent.com/nodesxploit/testnet/main/sui/tools/update_configs.sh && chmod +x update_configs.sh && ./update_configs.sh
```

## Usefull commands
Check sui node status
```
service suid status
```

Check node logs
```
journalctl -u suid -f -o cat
```

To delete node
```
sudo systemctl stop suid
sudo systemctl disable suid
sudo rm -rf ~/sui /var/sui/
sudo rm /etc/systemd/system/suid.service
```
