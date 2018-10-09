# BASiC : Blockchained Autonomous Social Infrastructure for Cities

This project aims to present a tool that combine an agent-based simulator with the blockchain Ethereum. This project contains 3 parts:

##### Agent-based simulator
The simulation represents the City of Cambridge and is made by using the [Gama Plateform](https://gama-platform.github.io/). The simulation is composed by cars and users.


##### Docker Container
In order to implement the Blockchain in an easy way, a [Docker container](https://docs.docker.com/install/) is used. 

##### Python Interface for the connection 
The connection between the simulation and the blockchain is made by using a [Python](https://www.python.org/downloads/) Interface.

## Getting Started
### Prerequisites
First, clone this repesitory.

```
$ git clone https://github.com/agrignard/BlockCar.git
```

You will need to have [Python](https://www.python.org/downloads/), [Docker](https://docs.docker.com/install/) and [Gama](https://gama-platform.github.io/) installed on your computer.


### Running the app

#### 1. Run the docker composer

Go inside the docker folder and and run an Ethereum Docker cluster by running the following:

```
$ docker-compose up -d
```

By default this will create:

* 1 Ethereum Bootstrapped container
* 1 Ethereum node (which connects to the bootstrapped container on launch)
* 1 Netstats container (with a Web UI to view activity in the cluster)
* 16 accounts pre-filled with Ether (you can modify or create more accounts by looking at `files/genesis.json`.) 


To access the Netstats Web UI:

```
open http://$(docker-machine ip default):3000
```

Each car of the simulation is a node. Thus, the number of docker containers needed must be same as the number of cars you want to create in the simulation. You can scale the number of Ethereum nodes by running:

```
docker-compose scale eth=3
``` 

You need to have at least one node mining. To get attached to the `geth` JavaScript console on the node you can run the following
```
docker exec -it docker-geth-network-master_eth_1 geth attach ipc://root/.ethereum/devchain/geth.ipc
```
Then you can `miner.start()`, and then check to see if it's mining by inspecting `web3.eth.mining`. 

See the [Javascript Runtime](https://github.com/ethereum/go-ethereum/wiki/JavaScript-Console) docs for more.


#### 2. Run the python server

In the PythonInterface folder, run :

```
py connection_interface.py
``` 
#### 3. Run the simulation

Import the CityScope Project in the Gama interface and make sure that the number of cars is equal to the number of node. When it's done, launch the experiments. Before to be able to start it, wait that each car deployed his smart contract. You will receive a confirmation message in the Python console with the address of the deployed smart contract. When the smart contracts are all deployed, you can start the simulation.
 
---
