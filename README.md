# Blockfrost bootstrap

Blockfrost bootstrap is a toolkit that helps you to deploy a Blockfrost cluster in minutes.

<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#Installation">Installation</a> •
  <a href="#usage">How To Use</a> •
  <a href="#contributing">Contributing</a>
</p>

## Key Features

A ready to go Blockfrost instance.

- Cardano Node
- Cardano Db Sync with Postgres database
- Cardano Submit API
- Ogmios
- Sprinkle some Blockfrost Backend on top of it

## Installation

The bootstrap cluster is supposed to be a development tool and we do not recommend using it as a production deployment. It's at your
own risk.

You need to have `docker` and `docker-compose` installed on your system. We recommend at least 64GB of memory.

```bash
# Clone this repository
$ git clone --recurse-submodules https://github.com/blockfrost/blockfrost-bootstrap

# Go into the repository
$ cd blockfrost-bootstrap

# Run the bootstrap script
$ ./blockfrost-bootstrap
Usage: ./blockfrost-bootstrap {init|start|stop|status|height|destroy}

    init      Initialize an blockfrost bootstrap cluster
    start     Start the cluster
    stop      Stop the cluster
    status    Get status of an initialized cluster
    height    Get current height of the cluster
    destroy   Destroy the current cluster
```

## Usage

### Initializing your cluster

![Blockfrost bootstrap](.github/assets/demo.gif)

### Starting and stopping your cluster

Use the `start` and `stop` commands.

```
$ ./blockfrost-bootstrap stop
Stopping blockfrost-bootstrap_cardano-submit-api_1     ... done
Stopping blockfrost-bootstrap_postgres_1               ... done
Stopping blockfrost-bootstrap_blockfrost-backend-ryo_1 ... done
Stopping blockfrost-bootstrap_cardano-db-sync_1        ... done
Stopping blockfrost-bootstrap_ogmios_1                 ... done
Stopping blockfrost-bootstrap_cardano-node_1           ... done
$
```

### Query Blockfrost

```bash
$ curl http://localhost:3000/blocks/latest | jq
{
  "time": 1704646432,
  "height": 1789685,
  "hash": "8b71facfbdf47f11f1dddd514eb20dd46d92417be9be5cbbf9d5ab7ea1d22826",
  "slot": 48963232,
  "epoch": 117,
  "epoch_slot": 60832,
  "slot_leader": "pool1upqfyzqpk6wkpsvw90qqrpr9tjyemh484wk4em69anwpu586ehq",
  "size": 4,
  "tx_count": 0,
  "output": null,
  "fees": null,
  "block_vrf": "vrf_vk1suxu5crrj7u96tjwu8jxhkum0p9qj2s7cfwts9rv7szxg4hlscwqg9ljpt",
  "op_cert": "ada64e38de0a5e795b69bcb6b2598142983ef36d348d36f0a0541362811e4eb0",
  "op_cert_counter": "5",
  "previous_block": "cdaefafd740d041fc89e8392f8397ff88c3d3053d236c7b3200f7b164d4344e5",
  "next_block": null,
  "confirmations": 0
}
```

### Status of the cluster

You can view the current status of your cluster using the `status` command.

```
$ ./blockfrost-bootstrap status
NAMES                                           CONTAINER ID   STATUS                             PORTS
blockfrost-bootstrap_cardano-submit-api_1       d07dd8b5aada   Up 34 seconds (healthy)            0.0.0.0:8090->8090/tcp, :::8090->8090/tcp
blockfrost-bootstrap_postgres_1                 ee48c946b6b7   Up 34 seconds (healthy)            0.0.0.0:5432->5432/tcp, :::5432->5432/tcp
blockfrost-bootstrap_blockfrost-backend-ryo_1   76294d3e2861   Up 34 seconds (health: starting)   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp
blockfrost-bootstrap_cardano-db-sync_1          cadae3918431   Up 34 seconds
blockfrost-bootstrap_ogmios_1                   cb625defb5c1   Up 34 seconds (healthy)            0.0.0.0:1337->1337/tcp, :::1337->1337/tcp
blockfrost-bootstrap_cardano-node_1             c9682a6a1510   Up 35 seconds (healthy)
$
```

## Contributing

Contributions do this repository are welcome. If you would like to contribute, please open a pull request to this repository and someone will review
it as soon as possible.
