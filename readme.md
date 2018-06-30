# Geth

Simple getting started of ethereum

## Download geth

https://geth.ethereum.org/downloads/ 

Geth/v1.7.2-stable-1db4ecdc/windows-amd64/go1.9

** you can use this in newers versions

## Create Genesis json
genesis.json >>

{
    "config": {
        "chainId": 1234,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "difficulty": "0x1",
    "gasLimit": "0xFFFFFF",
    "coinbase":"0x3333333333333333333333333333333333333333",
    "alloc": {}
}


## Create password file
	echo password >> password

## Create a data directory
	mkdir datadir

## Create an Ethereum account
	./geth.exe --password password --datadir datadir account new

## Init genesis
	 ./geth.exe --datadir datadir init genesis.json

## Run with GethStartupProcedure.js

### Run with first account locked
    ./geth.exe --networkid 1234 --rpc --rpccorsdomain "*" --rpcapi="db,eth,net,web3,personal,web3" --datadir datadir js GethStartupProcedure.js

use this function into geth console to unlock account:

    web3.eth.personal.unlockAccount("address", "password", 0)


### Run with first account Unlocked 

    ./geth.exe --password password --networkid 1234 --ws --wsport 8546 --wsorigins "*" --rpc --rpccorsdomain "*" --rpcapi="db,eth,net,web3,personal,web3" --unlock 0 --datadir datadir js GethStartupProcedure.js

## Run without GethStartupProcedure.js

### Run with first account locked
    ./geth.exe --networkid 1234 --rpc --rpccorsdomain "*" --rpcapi="db,eth,net,web3,personal,web3" --datadir datadir --mine --minerthreads=4 --etherbase < your account >

use this function into geth console to unlock account:

    web3.eth.personal.unlockAccount("address", "password", 0)

use this function into geth console to set Etherbase:

    miner.setEtherbase(' < your account > ');


### Run with first account Unlocked 

    ./geth.exe --password password --networkid 1234 --ws --wsport 8546 --wsorigins "*" --rpc --rpccorsdomain "*" --rpcapi="db,eth,net,web3,personal,web3" --unlock 0 --datadir datadir --mine --minerthreads=4 --etherbase < your account >

use this function into geth console to set Etherbase:

    miner.setEtherbase(' < your account > ');


## compile contract

* use remix: https://remix.ethereum.org/
    to connect with you node
        127.0.0.1:8545

* compile the contract simpleStorage.sol!!

## Add peer

Do the same steps to create the ethereum chain but without run, then check the bootnode in the first console

you will see something like this:


    UDP listener up self=enode://6976b631e81e241bc59ecc5b491c555ad388a6f0a21fba04b3bd79563b03fccf1dc8dbc504efbdce7b03ae26331db6760fadbb7b9b3bf77b153cd741e27dde8c@0.0.0.0:30303


then create a static node file with the enode obtained previously


    echo "[\"enode://6976b631e81e241bc59ecc5b491c555ad388a6f0a21fba04b3bd79563b03fccf1dc8dbc504efbdce7b03ae26331db6760fadbb7b9b3bf77b153cd741e27dde8c@127.0.0.1:30303\"]" > ./datadir/geth/static-nodes.json


then if you are in localhost change the ports numbers if not you can already run:


    ./geth.exe --password password --networkid 1234 --ws --wsport 8548 --wsorigins "" --rpc --rpccorsdomain "" --rpcapi="db,eth,net,web3,personal,web3" --unlock 0 --datadir datadir --port 30304 --rpc --rpcport 8547 --ipcdisable js GethStartupProcedure.js


If everything works in the first geth console you will see "Block synchronisation started" and some imports