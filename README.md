# Polkadot P2P testing proof-of-concept

This is a proof of concept take advantage of the already standard way of communicating with nodes : P2P mesages. Using libp2p we could feed a node with blocks, transactions, or even send incorrect transactions and verify their behaviors accross all the implementations. This doesn't require modifying the node in anyway and allow a good granularity of tests. Our PoC, just connect to a polkadot node and tests its ping interfaces (which is part of the spec).

## Running tests

You can run all the test from one command on the node you want. Currently we support the following nodes:
    * Polkadot
    * Gossamer

Example: 
```shell
$ make test node=polkadot
```
Wait for the split screen to show and for the for the first blocks to be generated. (for gossamer, please use `node=gossamer`)

Then you can start the test
```
$ npm start
```

## Notes

### Monitor dev node

Can check a bunch of information on the node on https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944%2Fwestend#/rpc
Even if it run locally.

### Start docker container

#### Polkadot
```
$ docker build -t polkadot -f Dockerfile.polkadot .
$ docker run -d -p 30333:30333 -p 9944:9944 -v ./misc/chainspec:/tmp/chainspec polkadot
```

#### Gossamer
```
$ docker build -t gossamer -f Dockerfile.gossamer .
$ docker run -d -p 30333:30333 -p 9944:9944 gossamer
```

### Run the test

In a new terminal, you can run the javascript program. Using `DEBUG=libp2p,libp2p:*` shows the libp2p logs in detail to have a better following of the underlying operations.

```
$ npm install
$ DEBUG=libp2p,libp2p:* npm start
```