<p align="center">
  <a href="https://kyve.network">
    <img src="https://user-images.githubusercontent.com/62398724/137493477-63868209-a19b-4efa-9413-f06d41197d6d.png" style="border-radius: 50%" height="96">
  </a>
  <h3 align="center"><code>@kyve/evm</code></h3>
  <p align="center">✅ The official KYVE EVM integration.</p>
</p>

> Note: The whole documentation on how to run a protocol node can be found [here](https://docs.kyve.network/intro/protocol-node.html)

## Requirements

Wallets

- A [Keplr](https://keplr.app) wallet with $KYVE. (You can claim some [here](https://app.kyve.network/faucet))
- An [Arweave](https://arweave.org/) keyfile with some AR. (You can claim some [here](https://faucet.arweave.net/))
Minimum hardware requirements

- Ubuntu 20.04
- 1vCPU
- 4GB RAM
- 1GB DISK

### update all packages and install unzip

```
sudo apt update && apt install unzip
```

Create a directory, go there and download the binary

```
mkdir -p /home/kyve
cd /home/kyve && wget https://github.com/KYVENetwork/evm/releases/download/v1.0.3/evm-linux.zip && unzip evm-linux.zip
```

> version check
```
cd /home/kyve && ./evm-linux --version
```

### make the binary executable

```
chmod +x evm-linux
```

###  Building

Copy the json to the /home/kyve folder, after renaming your json file to arweave.json

Next we create the service. We change only your data, marked below.

```
sudo tee /etc/systemd/system/kyved.service > /dev/null <<EOF
[Unit]
Description=Kyve Node
After=network-online.target
[Service]
User=root
WorkingDirectory=/home/kyve/
ExecStart=/home/kyve/evm-linux -m “mnemonic phrase” -k /home/kyve/arweave.json -p 0 or 1 -v -s your amount stake
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```

### Next, we start our service

```
sudo systemctl daemon-reload
sudo systemctl enable kyved
sudo systemctl start kyved
```
### View logs
```
journalctl -f -u kyved
```
### Congratulations, you have become a validator!





