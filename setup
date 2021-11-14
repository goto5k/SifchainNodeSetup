# Install Sifchain Full Node from scratch (chain-id: sifchain-1)

<!-- MarkdownTOC autolink="true" -->

- [Pre-requisites](#pre-requisites)
	- [User account](#user-account)
	- [Go deployment](#go-deployment)
		- [Download and extract repository](#download-and-extract-repository)
		- [Add Go environmental variables](#add-go-environmental-variables)
- [Cosmovisor](#cosmovisor)
	- [Create folders](#create-folders)
	- [Build Cosmovisor](#build-cosmovisor)
	- [Prepare binaries to run node](#prepare-binaries-to-run-node)
		- [0.9.0](#090)
		- [0.9.1](#091)
		- [0.9.5](#095)
		- [0.9.7](#097)
		- [0.9.10](#0910)
		- [0.9.12](#0912)
- [Node initialization](#node-initialization)
	- [Initialize config](#initialize-config)
	- [Genesis](#genesis)
	- [Add peers](#add-peers)
- [Start node](#start-node)
	- [Add service to systemd configuration](#add-service-to-systemd-configuration)
	- [Start service](#start-service)
- [Monitor status](#monitor-status)

<!-- /MarkdownTOC -->

**NOTE:** Please note that for purpose of running Sifchain Validator/Node dedicated user has been created called ***sifchain***.


# Pre-requisites

## User account
```bash
sudo adduser sifchain
```
**NOTE:** All further steps have to be performed as ***sifchain*** user


## Go deployment

### Download and extract repository
```bash
GOVER=$(curl https://golang.org/VERSION?m=text)
wget https://golang.org/dl/${GOVER}.linux-amd64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf ${GOVER}.linux-amd64.tar.gz
```
**NOTE**: That will install latest version of Go


### Add Go environmental variables
Set of variables, which should be set for user(s) with need to build Go apps.

That can be placed in ```${HOME}/.profile``` or ```${HOME}/.bashrc``` or any other shell-specific file, whic sets variable during logon
```bash
# add environmental variables for Go
if [ -f "/usr/local/go/bin/go" ] ; then
    export GOROOT=/usr/local/go
    export GOPATH=${HOME}/go
    export GOBIN=$GOPATH/bin
    export PATH=${PATH}:${GOROOT}/bin:${GOBIN}
fi
```

**NOTE:** Once all changes are applied and files installed make sure all shell instances will be closed and then logoff and logon again to system. That way all environmental variables will be set correctly.



# Cosmovisor


## Create folders
```bash
mkdir -p ${HOME}/.local/bin
mkdir -p ${HOME}/.sifnoded/cosmovisor/genesis/bin
mkdir -p ${HOME}/.sifnoded/cosmovisor/upgrades
mkdir -p ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.1/bin
mkdir -p ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.5/bin
mkdir -p ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.7/bin
mkdir -p ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.10/bin
mkdir -p ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.12/bin
```
Appropriate versions of Sifchain binaries must be placed in appropriate folders.


**NOTE:** All steps done as ***sifchain*** user.


## Build Cosmovisor
```bash
cd ${HOME}
git clone https://github.com/cosmos/cosmos-sdk && cd cosmos-sdk/cosmovisor/
make
cp cosmovisor ${HOME}/.local/bin
```
**NOTE:** all steps done as ***sifchain*** user.


## Prepare binaries to run node

### 0.9.0
```bash
cd ${HOME}
wget https://github.com/Sifchain/sifnode/releases/download/mainnet-0.9.0/sifnoded-mainnet-0.9.0-linux-amd64.zip
unzip sifnoded-betanet-0.9.0-linux-amd64.zip -d ${HOME}/.sifnoded/cosmovisor/genesis/bin
```

### 0.9.1
```bash
cd ${HOME}
wget https://github.com/Sifchain/sifnode/releases/download/betanet-0.9.1/sifnoded-betanet-0.9.1-linux-amd64.zip
unzip sifnoded-betanet-0.9.1-linux-amd64.zip -d ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.1/bin
```

### 0.9.5
```bash
cd ${HOME}
wget https://github.com/Sifchain/sifnode/releases/download/betanet-0.9.5/sifnoded-betanet-0.9.5-linux-amd64.zip
unzip sifnoded-betanet-0.9.5-linux-amd64.zip -d ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.5/bin
```

### 0.9.7
```bash
cd ${HOME}
wget https://github.com/Sifchain/sifnode/releases/download/betanet-0.9.7/sifnoded-betanet-0.9.7-linux-amd64.zip
unzip sifnoded-betanet-0.9.7-linux-amd64.zip -d ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.7/bin
```

### 0.9.10
```bash
cd ${HOME}
wget https://github.com/Sifchain/sifnode/releases/download/betanet-0.9.10/sifnoded-betanet-0.9.10-linux-amd64.zip
unzip sifnoded-betanet-0.9.10-linux-amd64.zip -d ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.10/bin
```

### 0.9.12
```bash
cd ${HOME}
wget https://github.com/Sifchain/sifnode/releases/download/betanet-0.9.12/sifnoded-betanet-0.9.12-linux-amd64.zip
unzip sifnoded-betanet-0.9.12-linux-amd64.zip -d ${HOME}/.sifnoded/cosmovisor/upgrades/0.9.12/bin
```


# Node initialization

## Initialize config
```bash
${HOME}/.sifnoded/cosmovisor/genesis/bin/sifnoded init <MONIKER> --chain-id sifchain-1
```
**NOTE:** Replace <MONIKER> with name of the node you want to have.


## Genesis
```bash
cd ${HOME}
wget https://github.com/Sifchain/networks/raw/master/betanet/sifchain-1/genesis.json.gz
gzip -dc ${HOME}/genesis.json.gz ${HOME}/.sifnoded/config/genesis.json
```


## Add peers

[List of persistent peers provided by project team](https://github.com/Sifchain/networks/blob/master/betanet/sifchain-1/persistent_peers.md)

Add those as comma separated to ***config.toml***
```bash
nano ${HOME}/.sifnoded/config/config.toml
```

Locate line ***persistent_peers = ""*** and add peers:
```bash
persistent_peers = "0d4981bdaf4d5d73bad00af3b1fa9d699e4d3bc0@44.235.108.41:26656,bcc2d07a14a8a0b3aa202e9ac106dec0bef91fda@13.55.247.60:26656,663dec65b754aceef5fcccb864048305208e7eb2@34.248.110.88:26656,0120f0a48e7e81cc98829ef4f5b39480f11ecd5a@52.76.185.17:26656,6535497f0152293d773108774a705b86c2249a9c@44.238.121.65:26656,fdf5cffc2b20a20fab954d3b6785e9c382762d14@34.255.133.248:26656,8c240f71f9e060277ce18dc09d82d3bbb05d1972@13.211.43.177:26656,9fbcb6bd5a7f20a716564157c4f6296d2faf5f64@18.138.208.95:26656"
```


# Start node

## Add service to systemd configuration
Create service file **/lib.systemd/system/sifchain.service** with following content:

```bash
sudo nano /lib/systemd/system/sifchain.service
```
**NOTE:** Below service configuration assumes that user ***sifchain*** has been created for Validator/Node. If you have different user, adjust file accordingly.

```bash
[Unit]
Description=Sifchain Validator (Cosmovisor)
After=network-online.target

[Service]
User=sifchain
Group=sifchain
ExecStart=/home/sifchain/.local/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=4096
Environment="DAEMON_NAME=sifnoded"
Environment="DAEMON_HOME=/home/sifchain/.sifnoded"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="DAEMON_LOG_BUFFER_SIZE=512"

[Install]
WantedBy=multi-user.target
```

## Start service
Reload ***systemd*** configuration and enable ***sifchain*** service.
```bash
sudo systemctl daemon-reload
sudo systemctl enable sifchain.service
sudo systemctl start sifchain.service
```


# Monitor status
To see progress of synchronization
```bash
journalctl -u sifchain -f
```
Command will keep displaying all activity done by ***sifchain.service***.
