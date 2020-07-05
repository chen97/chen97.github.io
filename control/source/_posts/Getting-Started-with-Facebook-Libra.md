---
title: Getting Started with Facebook Libra
date: 2019-06-25 19:39:12
categories:
- Technology
tags: 
- Libra
- Linux
- Block-Chain
---

Facebook has rolled out its ambitious plans for a new currency and financial infrastructure that could make our transactions easier. Libra is a new type of cryptocurrency that using blockchain technology to allow you to make purchases and send money online with almost zero fees. The idea is to provide fast and reliable transactions with the option to hide your identity while exchanging from your local currency to use Facebook’s Calibra wallet.Now, Libra fullfills the requirements of developer in order to enter the blockchain era. I tried to build a Libra environment to simulate the trading step of the Libra and it was guided by the online resources which will mention in the end of article.

<!-- more --> 

## Environment Setup

### Requirement of Environment

>
> Linux Ubuntu 18.04 LTS, 4GB Memory, 100G Storage
>

### Update Linux
```
sudo apt-get update && sudo apt-get upgrade
```

## Download Libra and Related Packages

### Download Libra
```
git clone https://github.com/libra/libra.git
```

### Install Golang
Use the wget to downlaod package and do extraction.
```
wget https://studygolang.com/dl/golang/go1.12.5.linux-amd64.tar.gz
tar -xvf go1.12.5.linux-amd64.tar.gz
```
Configure the environment variable
```
vim /etc/profile
```
Insert the environment path
```
export GOROOT=/usr/go
export GOPATH=/usr/gopath
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

### Install Rust and related software
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
rustup toolchain install nightly-2019-05-22-x86_64-unknown-linux-gnu
rustup override set nightly-2019-05-22
```
Check the version after the intallation
```
rustc --version
rustup --version
```

### Install cmake
```
sudo apt-get install cmake
```

### Configuration of protocol
```
wget https://github.com/protocolbuffers/protobuf/releases/download/v3.6.1/protobuf-all-3.6.1.tar.gz
tar -xvf protobuf-all-3.6.1.tar.gz
cd protobuf-3.6.1/
./configure
make
make check
sudo make install
protoc --version
# show：libprotoc 3.6.1
```

## Installation of Libra
```
cd libra
./scripts/dev_setup.sh
```
Showing
```
Installing CMake......
CMake is already installed
Installing Go......
Go is already installed
Installing Protobuf......
Protobuf is already installed

Finished installing all dependencies.

You should now be able to build the project by running:
	source /root/.cargo/env
	cargo build
```

## Play with Libra

### Build Libra CLI Client and Connect to the Testnet
```
./scripts/cli/start_cli_testnet.sh
```
After finish the Testnet showing:
![Result after the CLI Client build](/1.png)

### Create an account and check the status

Create two account 
```
account create
account create
```
Check the details of account
```
account list
```
![Create and check account](/2.png)

### Insert money to the account
We insert 101 coins to first account and, 51 coins to the second account.
```
account mint 0 101
account mint 0 51
```
Check the balance
```
query balance 0
query balance 1
```
![Insert and check the balance of account](/3.png)

### Trade the coins
So far, we can starting to do the exchange between two accounts.
We transfer 33 coins from first account to second account.
```
transfer 0 1 33
```
![trading of the two account](/5.png)

## Refferences
* Libra official website:  https://libra.org/en-US/
* Libra white paper: https://libra.org/en-US/white-paper/
* Libra technical white paper: https://developers.libra.org/docs/assets/papers/the-libra-blockchain.pdf
* Libra developer documentation: https://developers.libra.org/
* Libra Github: https://github.com/libra/libra
* Tutorial of environment setup: https://developers.libra.org/docs/my-first-transaction



