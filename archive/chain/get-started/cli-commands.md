---
id: cli-commands
title: CLI Commands
description: "List of CLI commands and command flags for Metabit Chain."
keywords:
  - docs
  - metabit
  - chain
  - cli
  - commands
  - flags
---

This section details the present commands, command flags in the Metabit Chain, and how they're used.

:::tip JSON output support

The `--json` flag is supported on some commands. This flag instructs the command to print the output in JSON format

:::

## Startup Commands

| **Command**       | **Description**                                                                                                                                                 |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| server            | The default command that starts the blockchain client, by bootstrapping all modules together                                                                    |
| genesis           | Generates a *genesis.json* file, which is used to set a predefined chain state before starting the client. The structure of the genesis file is described below |
| genesis predeploy | Predeploys a Smart Contract for fresh networks                                                                                                                  |

### server flags


| **All server flags**                                                                        |
|---------------------------------------|---------------------------------------------|
| [data-dir]| [jsonrpc] |
| [json-rpc-block-range-limit] | [json-rpc-batch-request-limit] |
|[grpc]| [libp2p] | 
| [prometheus]| [block-gas-target] | 
| [max-peers] | [max-inbound-peers]|
| [max-outbound-peers] | [max-enqueued] |
| [log-level] | [log-to] |
| [chain] | [join] |
| [nat] | [dns] | 
| [price-limit] | [max-slots] |
| [config] | [secrets-config] | 
| [dev] | [dev-interval] | 
| [no-discover] | [restore] | 
| [block-time] | [access-control-allow-origins] |


#### <h4><i>data-dir</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--data-dir DATA_DIRECTORY]

  </TabItem>
  <TabItem value="example" label="Example">

    server --data-dir ./example-dir

  </TabItem>
</Tabs>

Used to specify the data directory used for storing Metabit Chain client data. Default: `./test-chain`.

---


#### <h4><i>jsonrpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--jsonrpc JSONRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --jsonrpc 127.0.0.1:10000

  </TabItem>
</Tabs>

Sets the address and port for the JSON-RPC service `address:port`.   
If only port is defined `:10001` it will bind to all interfaces `0.0.0.0:10001`.   
If omitted the service will bind to the default `address:port`.   
Default address: `0.0.0.0:8545`.

---

#### <h4><i>json-rpc-block-range-limit</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--json-rpc-block-range-limit BLOCK_RANGE]

  </TabItem>
  <TabItem value="example" label="Example">

    server --json-rpc-block-range-limit 1500

  </TabItem>
</Tabs>

Sets the maximum block range to be considered when executing json-rpc requests that include fromBlock/toBlock values (e.g. eth_getLogs).  
This limit can be completely disabled by setting the value to `0`. Default:`1000`.

---

#### <h4><i>json-rpc-batch-request-limit</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--json-rpc-batch-request-limit MAX_LENGTH]

  </TabItem>
  <TabItem value="example" label="Example">

    server --json-rpc-batch-request-limit 50

  </TabItem>
</Tabs>

Sets the maximum length to be considered when handling json-rpc batch requests.
This limit can be completely disabled by setting the value to `0`. Default: `20`.

---

#### <h4><i>grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --grpc-address 127.0.0.1:10001

  </TabItem>
</Tabs>

Sets the address and port for the gRPC service `address:port`. Default address: `127.0.0.1:9632`.

---

#### <h4><i>libp2p</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--libp2p LIBP2P_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --libp2p 127.0.0.1:10002

  </TabItem>
</Tabs>

Sets the address and port for the libp2p service `address:port`. Default address: `127.0.0.1:1478`.

---

#### <h4><i>prometheus</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--prometheus PROMETHEUS_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --prometheus 127.0.0.1:10004

  </TabItem>
</Tabs>

Sets the address and port for the prometheus server `address:port`.   
If only port is defined `:5001` the service will bind to all interfaces `0.0.0.0:5001`.   
If omitted the service will not be started.

---

#### <h4><i>block-gas-target</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--block-gas-target BLOCK_GAS_TARGET]

  </TabItem>
  <TabItem value="example" label="Example">

    server --block-gas-target 10000000

  </TabItem>
</Tabs>

Sets the target block gas limit for the chain. Default (not enforced): `0`.

---

#### <h4><i>max-peers</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--max-peers PEER_COUNT]

  </TabItem>
  <TabItem value="example" label="Example">

    server --max-peers 40

  </TabItem>
</Tabs>

Sets the client's maximum peer count. Default: `40`.

Peer limit should be specified either by using `max-peers` or `max-inbound/outbound-peers` flag.

---

#### <h4><i>max-inbound-peers</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--max-inbound-peers PEER_COUNT]

  </TabItem>
  <TabItem value="example" label="Example">

    server --max-inbound-peers 32

  </TabItem>
</Tabs>

Sets the client's maximum inbound peer count. If `max-peers` is set, max-inbound-peer limit is calculated using the following formulae.

`max-inbound-peer = InboundRatio * max-peers`, where `InboundRatio` is `0.8`.

---

#### <h4><i>max-outbound-peers</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--max-outbound-peers PEER_COUNT]

  </TabItem>
  <TabItem value="example" label="Example">

    server --max-outbound-peers 8

  </TabItem>
</Tabs>

Sets the client's maximum outbound peer count. If `max-peers` is set, max-outbound-peer count is calculated using the following formulae.

`max-outbound-peer = OutboundRatio * max-peers`, where `OutboundRatio` is `0.2`.

---

#### <h4><i>max-enqueued</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--max-enqueued ENQUEUED_TRANSACTIONS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --max-enqueued 210

  </TabItem>
</Tabs>

Sets the maximum number of enqueued transactions per account. Default:`128`.

---

#### <h4><i>log-level</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--log-level LOG_LEVEL]

  </TabItem>
  <TabItem value="example" label="Example">

    server --log-level DEBUG

  </TabItem>
</Tabs>

Sets the log level for console output. Default: `INFO`.

---

#### <h4><i>log-to</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--log-to LOG_FILE]

  </TabItem>
  <TabItem value="example" label="Example">

    server --log-to node.log

  </TabItem>
</Tabs>

Defines log file name that will hold all log output from the server command.
By default, all server logs will be outputted to console (stdout),
but if the flag is set, there will be no output to the console when running server command.

---

#### <h4><i>chain</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--chain GENESIS_FILE]

  </TabItem>
  <TabItem value="example" label="Example">

    server --chain /home/ubuntu/genesis.json

  </TabItem>
</Tabs>

Specifies the genesis file used for starting the chain. Default: `./genesis.json`.

---

#### <h4><i>join</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--join JOIN_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --join /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW

  </TabItem>
</Tabs>

Specifies the address of the peer that should be joined.

---

#### <h4><i>nat</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--nat NAT_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --nat 192.0.2.1

  </TabItem>
</Tabs>

Sets the external IP address without the port, as it can be seen by peers.

---

#### <h4><i>dns</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--dns DNS_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --dns dns4/example.io

  </TabItem>
</Tabs>

Sets the host DNS address. This can be used to advertise an external DNS. Supports `dns`,`dns4`,`dns6`.

---

#### <h4><i>price-limit</i></h4>


<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--price-limit PRICE_LIMIT]

  </TabItem>
  <TabItem value="example" label="Example">

    server --price-limit 10000

  </TabItem>
</Tabs>

Sets minimum gas price limit to enforce for acceptance into the pool. Default: `1`.

---

#### <h4><i>max-slots</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--max-slots MAX_SLOTS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --max-slots 1024

  </TabItem>
</Tabs>

Sets maximum slots in the pool. Default: `4096`.

---

#### <h4><i>config</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--config CLI_CONFIG_PATH]

  </TabItem>
  <TabItem value="example" label="Example">

    server --config ./myConfig.json

  </TabItem>
</Tabs>

Specifies the path to the CLI config. Supports `.json`.

---

#### <h4><i>secrets-config</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--secrets-config SECRETS_CONFIG]

  </TabItem>
  <TabItem value="example" label="Example">

    server --secrets-config ./secretsManagerConfig.json

  </TabItem>
</Tabs>

Sets the path to the SecretsManager config file. Used for Hashicorp Vault, AWS SSM and GCP Secrets Manager. If omitted, the local FS secrets manager is used.

---

#### <h4><i>dev</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--dev DEV_MODE]

  </TabItem>
  <TabItem value="example" label="Example">

    server --dev

  </TabItem>
</Tabs>

Sets the client to dev mode. Default: `false`. In dev mode, peer discovery is disabled by default.

---

#### <h4><i>dev-interval</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--dev-interval DEV_INTERVAL]

  </TabItem>
  <TabItem value="example" label="Example">

    server --dev-interval 20

  </TabItem>
</Tabs>

Sets the client's dev notification interval in seconds. Default: `0`.

---

#### <h4><i>no-discover</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--no-discover NO_DISCOVER]

  </TabItem>
  <TabItem value="example" label="Example">

    server --no-discover

  </TabItem>
</Tabs>

Prevents the client from discovering other peers. Default: `false`.

---

#### <h4><i>restore</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--restore RESTORE]

  </TabItem>
  <TabItem value="example" label="Example">

    server --restore backup.dat

  </TabItem>
</Tabs>

Restore blocks from the specified archive file

---

#### <h4><i>block-time</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--block-time BLOCK_TIME]

  </TabItem>
  <TabItem value="example" label="Example">

    server --block-time 1000

  </TabItem>
</Tabs>

Sets block production time in seconds. Default: `2`

---

#### <h4><i>access-control-allow-origins</i></h4>
<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    server [--access-control-allow-origins ACCESS_CONTROL_ALLOW_ORIGINS]

  </TabItem>
  <TabItem value="example" label="Example">

    server --access-control-allow-origins "https://metabitglobal.com"

  </TabItem>
</Tabs>

Sets the authorized domains to be able to share responses from JSON-RPC requests.   
Add multiple flags `--access-control-allow-origins "https://example1.com" --access-control-allow-origins "https://example2.com"` to authorize multiple domains.   
If omitted Access-Control-Allow-Origins header will be set to `*` and all domains will be authorized.

---

### genesis flags
| **All genesis flags**                                                                        |
|---------------------------------------|---------------------------------------------|
| [dir] | [name] |
| [pos] | [epoch-size] |
| [premine]| [chainid] |
| [ibft-validator-type] | [ibft-validators-prefix-path] |
| [ibft-validator]| [block-gas-limit] |
| [consensus] | [bootnode] |
| [max-validator-count] | [min-validator-count] |


#### <h4><i>dir</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--dir DIRECTORY]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --dir ./genesis.json

  </TabItem>
</Tabs>

Sets the directory for the Metabit Chain genesis data. Default: `./genesis.json`.

---

#### <h4><i>name</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--name NAME]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --name test-chain

  </TabItem>
</Tabs>

Sets the name for the chain. Default: `Metabit_chain`.

---

#### <h4><i>pos</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--pos IS_POS]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --pos

  </TabItem>
</Tabs>

Sets the flag indicating that the client should use Proof of Stake IBFT.
Defaults to Proof of Authority if flag is not provided or `false`.

---

#### <h4><i>epoch-size</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--epoch-size EPOCH_SIZE]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --epoch-size 50

  </TabItem>
</Tabs>

Sets the epoch size for the chain. Default `100000`.

---

#### <h4><i>premine</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--premine ADDRESS:VALUE]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --premine 0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000

  </TabItem>
</Tabs>

Sets the premined accounts and balances in the format `address:amount`.
The amount can be in either decimal or hex.
Default premined balance: `0xD3C21BCECCEDA1000000`(1 million native currency tokens).

---

#### <h4><i>chainid</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--chain-id CHAIN_ID]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --chain-id 200

  </TabItem>
</Tabs>

Sets the ID of the chain. Default: `100`.

---

#### <h4><i>ibft-validator-type</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--ibft-validator-type IBFT_VALIDATOR_TYPE]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --ibft-validator-type ecdsa

  </TabItem>
</Tabs>

Specifies the validation mode of block headers. Possible values: `[ecdsa, bls]`. Default: `bls`.

---

#### <h4><i>ibft-validators-prefix-path</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--ibft-validators-prefix-path IBFT_VALIDATORS_PREFIX_PATH]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --ibft-validators-prefix-path test-chain-

  </TabItem>
</Tabs>

Prefix path for validator folder directory. Needs to be present if the flag `ibft-validator` is omitted.

---

#### <h4><i>ibft-validator</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--ibft-validator IBFT_VALIDATOR_LIST]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --ibft-validator 0xC12bB5d97A35c6919aC77C709d55F6aa60436900

  </TabItem>
</Tabs>

Sets passed addresses as IBFT validators. Needs to be present if the flag `ibft-validators-prefix-path` is omitted.
1. If the network is running with ECDSA, the format is `--ibft-validator [ADDRESS]`. 
2. If the network is running with BLS, the format is  `--ibft-validator [ADDRESS]:[BLS_PUBLIC_KEY]`.

---

#### <h4><i>block-gas-limit</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--block-gas-limit BLOCK_GAS_LIMIT]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --block-gas-limit 5000000

  </TabItem>
</Tabs>

Refers to the maximum amount of gas used by all operations in a block. Default: `5242880`.

---

#### <h4><i>consensus</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--consensus CONSENSUS_PROTOCOL]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --consensus ibft

  </TabItem>
</Tabs>

Sets consensus protocol. Default: `pow`.

---

#### <h4><i>bootnode</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--bootnode BOOTNODE_URL]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --bootnode /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW

  </TabItem>
</Tabs>

Multiaddr URL for p2p discovery bootstrap. This flag can be used multiple times.
Instead of an IP address, the DNS address of the bootnode can be provided.

---

#### <h4><i>max-validator-count</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--max-validator-count MAX_VALIDATOR_COUNT]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --max-validator-count 42

  </TabItem>
</Tabs>

The maximum number of stakers able to join the validator set in a PoS consensus.
This number cannot exceed the value of MAX_SAFE_INTEGER (2^53 - 2).

---

#### <h4><i>min-validator-count</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--min-validator-count MIN_VALIDATOR_COUNT]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis --min-validator-count 4

  </TabItem>
</Tabs>

The minimum number of stakers needed to join the validator set in a PoS consensus.
This number cannot exceed the value of max-validator-count.
Defaults to 1.

---

### genesis predeploy flags

<h4><i>artifacts-path</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis predeploy [--artifacts-path PATH_TO_ARTIFACTS]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis predeploy --artifacts-path ./ArtifactsData.json

  </TabItem>
</Tabs>

Sets the path to the contract artifacts JSON that contains the `abi`, `bytecode` and `deployedBytecode`.

---

<h4><i>chain</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis predeploy [--chain PATH_TO_GENESIS]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis predeploy --chain ./genesis.json

  </TabItem>
</Tabs>

Sets the path to the `genesis.json` file that should be updated. Default `./genesis.json`.

---

<h4><i>constructor-args</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis predeploy [--constructor-args CONSTRUCTOR_ARGUMENT]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis predeploy --constructor-args 123

  </TabItem>
</Tabs>


---

<h4><i>predeploy-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis predeploy [--predeploy-address PREDEPLOY_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    genesis predeploy --predeploy-address 0x5555

  </TabItem>
</Tabs>

Sets the address to predeploy to. Default `0x0000000000000000000000000000000000001100`.

---


## Operator Commands

### Peer Commands

| **Command**            | **Description**                                                                     |
|------------------------|-------------------------------------------------------------------------------------|
| peers add   | Adds a new peer using their libp2p address                                  |
| peers list             | Lists all the peers the client is connected to through libp2p                      |
| peers status | Returns the status of a specific peer from the peers list, using the libp2p address |

<h3>peers add flags</h3>

<h4><i>addr</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    peers add --addr PEER_ADDRESS

  </TabItem>
  <TabItem value="example" label="Example">

    peers add --addr /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW

  </TabItem>
</Tabs>

Peer's libp2p address in the multiaddr format.

---

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    peers add [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    peers add --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>peers list flags</h3>

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    peers list [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    peers list --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>peers status flags</h3>

<h4><i>peer-id</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    peers status --peer-id PEER_ID

  </TabItem>
  <TabItem value="example" label="Example">

    peers status --peer-id 16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW

  </TabItem>
</Tabs>

Libp2p node ID of a specific peer within p2p network.

---

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    peers status [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    peers status --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

### IBFT Commands

| **Command**            | **Description**                                                                     |
|------------------------|-------------------------------------------------------------------------------------|
| ibft snapshot             | Returns the IBFT snapshot                    |
| ibft candidates  | Queries the current set of proposed candidates, as well as candidates that have not been included yet |
| ibft propose                | Proposes a new candidate to be added/removed from the validator set        |
| ibft status                | Returns the overall status of the IBFT client   |
| ibft switch                | Add fork configurations into genesis.json file to switch IBFT type |
| ibft quorum                | Specifies the block number after which the optimal quorum size method will be used for reaching consensus |


<h3>ibft snapshot flags</h3>

<h4><i>number</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft snapshot [--number BLOCK_NUMBER]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft snapshot --number 100

  </TabItem>
</Tabs>

The block height (number) for the snapshot.

---

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft snapshot [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft snapshot --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>ibft candidates flags</h3>

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft candidates [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft candidates --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>ibft propose flags</h3>

<h4><i>vote</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft propose --vote VOTE

  </TabItem>
  <TabItem value="example" label="Example">

    ibft propose --vote auth

  </TabItem>
</Tabs>

Proposes a change to the validator set. Possible values: `[auth, drop]`.

---

<h4><i>addr</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft propose --addr ETH_ADDRESS

  </TabItem>
  <TabItem value="example" label="Example">

    ibft propose --addr 0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7

  </TabItem>
</Tabs>

Address of the account to be voted for.

---

<h4><i>bls</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft propose --bls BLS_PUBLIC_KEY

  </TabItem>
  <TabItem value="example" label="Example">

    ibft propose --bls 0x9952735ca14734955e114a62e4c26a90bce42b4627a393418372968fa36e73a0ef8db68bba11ea967ff883e429b3bfdf

  </TabItem>
</Tabs>

BLS Public Key of the account to be voted for, necessary only in BLS mode.

---

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft candidates [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft candidates --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>ibft status flags</h3>

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft status [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft status --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>ibft switch flags</h3>

<h4><i>chain</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft switch [--chain GENESIS_FILE]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft switch --chain genesis.json

  </TabItem>
</Tabs>

Specifies the genesis file to update. Default: `./genesis.json`.

---

<h4><i>type</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft switch [--type TYPE]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft switch --type PoS

  </TabItem>
</Tabs>

Specifies the IBFT type to switch. Possible values: `[PoA, PoS]`.

---

<h4><i>deployment</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft switch [--deployment DEPLOYMENT]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft switch --deployment 100

  </TabItem>
</Tabs>

Specifies the height of contract deployment. Only available with PoS.

---

<h4><i>from</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft switch [--from FROM]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft switch --from 200

  </TabItem>
</Tabs>

---

<h4><i>ibft-validator-type</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

     ibft switch [--ibft-validator-type IBFT_VALIDATOR_TYPE]

  </TabItem>
  <TabItem value="example" label="Example">

     ibft switch --ibft-validator-type ecdsa

  </TabItem>
</Tabs>

Specifies the validation mode of block headers. Possible values: `[ecdsa, bls]`. Default: `bls`.

---

<h4><i>ibft-validators-prefix-path</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

     ibft switch [--ibft-validators-prefix-path IBFT_VALIDATORS_PREFIX_PATH]

  </TabItem>
  <TabItem value="example" label="Example">

     ibft switch --ibft-validators-prefix-path test-chain-

  </TabItem>
</Tabs>

Prefix path for the directories of new validators. Needs to be present if the flag `ibft-validator` is omitted. Available only when the IBFT mode is PoA (`--pos` flag is omitted).

---

<h4><i>ibft-validator</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

     ibft switch [--ibft-validator IBFT_VALIDATOR_LIST]

  </TabItem>
  <TabItem value="example" label="Example">

     ibft switch --ibft-validator 0xC12bB5d97A35c6919aC77C709d55F6aa60436900

  </TabItem>
</Tabs>

Sets passed in addresses as IBFT validators used after the fork. Needs to be present if the flag `ibft-validators-prefix-path` is omitted. Available only in PoA mode.
1. If the network is running with ECDSA, the format is `--ibft-validator [ADDRESS]`. 
2. If the network is running with BLS, the format is  `--ibft-validator [ADDRESS][BLS_PUBLIC_KEY]`.

---

<h4><i>max-validator-count</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft switch [--max-validator-count MAX_VALIDATOR_COUNT]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft switch --max-validator-count 42

  </TabItem>
</Tabs>

The maximum number of stakers able to join the validator set in a PoS consensus.
This number cannot exceed the value of MAX_SAFE_INTEGER (2^53 - 2).

---

<h4><i>min-validator-count</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft switch [--min-validator-count MIN_VALIDATOR_COUNT]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft switch --min-validator-count 4

  </TabItem>
</Tabs>

The minimum number of stakers needed to join the validator set in a PoS consensus.
This number cannot exceed the value of max-validator-count.
Defaults to 1.

Specifies the beginning height of the fork.

---

<h3>ibft quorum flags</h3>

<h4><i>from</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft quorum [--from your_quorum_switch_block_num]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft quorum --from 350

  </TabItem>
</Tabs>

The height to switch the quorum calculation to QuorumOptimal, which uses the formula `(2/3 * N)`, `N` being the number of validator nodes. Please note that this is for backwards compatibility, ie. only for chains that used a Quorum legacy calculation up to a certain block height.

---

<h4><i>chain</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    ibft quorum [--chain GENESIS_FILE]

  </TabItem>
  <TabItem value="example" label="Example">

    ibft quorum --chain genesis.json

  </TabItem>
</Tabs>

Specifies the genesis file to update. Default: `./genesis.json`.

### Transaction Pool Commands

| **Command**            | **Description**                                                                      |
|------------------------|--------------------------------------------------------------------------------------|
| txpool status          | Returns the number of transactions in the pool                                       |
| txpool subscribe       | Subscribes for events in the transaction pool                                        |

<h3>txpool status flags</h3>

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    txpool status [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    txpool status --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>txpool subscribe flags</h3>

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    txpool subscribe [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    txpool subscribe --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

---

<h4><i>promoted</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    txpool subscribe [--promoted LISTEN_PROMOTED]

  </TabItem>
  <TabItem value="example" label="Example">

    txpool subscribe --promoted

  </TabItem>
</Tabs>

Subscribes for promoted tx events in the TxPool.

---

<h4><i>dropped</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    txpool subscribe [--dropped LISTEN_DROPPED]

  </TabItem>
  <TabItem value="example" label="Example">

    txpool subscribe --dropped

  </TabItem>
</Tabs>

Subscribes for dropped tx events in the TxPool.

---

<h4><i>demoted</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    txpool subscribe [--demoted LISTEN_DEMOTED]

  </TabItem>
  <TabItem value="example" label="Example">

    txpool subscribe --demoted

  </TabItem>
</Tabs>

Subscribes for demoted tx events in the TxPool.

---

<h4><i>added</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    txpool subscribe [--added LISTEN_ADDED]

  </TabItem>
  <TabItem value="example" label="Example">

    txpool subscribe --added

  </TabItem>
</Tabs>

Subscribes for added tx events to the TxPool.

---

<h4><i>enqueued</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    txpool subscribe [--enqueued LISTEN_ENQUEUED]

  </TabItem>
  <TabItem value="example" label="Example">

    txpool subscribe --enqueued

  </TabItem>
</Tabs>

Subscribes for enqueued tx events in the account queues.

---

### Blockchain commands

| **Command**            | **Description**                                                                     |
|------------------------|-------------------------------------------------------------------------------------|
| status                 | Returns the status of the client. The detailed response can be found below          |
| monitor                | Subscribes to a blockchain event stream. The detailed response can be found below   |
| version                | Returns the current version of the client |

<h3>status flags</h3>

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    status [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    status --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

<h3>monitor flags</h3>

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    monitor [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    monitor --grpc-address 127.0.0.1:10003

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

---
<h3>version command</h3>


<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    version

  </TabItem>
</Tabs>

Displays release version, git branch, commit hash and build time.

## Secrets Commands

| **Command** | **Description**                                                                                                                                      |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| secrets init      | Initializes the private keys to the corresponding secrets manager                                                         |
| secrets generate         | Generates a secrets manager configuration file which can be parsed by the Metabit Chain    |
| secrets output    | Prints the BLS public key address, validator public key address, and node id for reference |

### secrets init flags

<h4><i>config</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets init [--config SECRETS_CONFIG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets init --config ./secretsManagerConfig.json

  </TabItem>
</Tabs>

Sets the path to the SecretsManager config file. Used for Hashicorp Vault. If omitted, the local FS secrets manager is used.

---

<h4><i>data-dir</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets init [--data-dir DATA_DIRECTORY]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets init --data-dir ./example-dir

  </TabItem>
</Tabs>

Sets the directory for the Metabit Chain data if the local FS is used.

---

<h4><i>ecdsa</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets init [--ecdsa FLAG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets init --ecdsa=false

  </TabItem>
</Tabs>

Sets the flag indicating whether to generate an ECDSA key. Default: `true`.

---

<h4><i>network</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets init [--network FLAG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets init --network=false

  </TabItem>
</Tabs>

Sets the flag indicating whether to generate a Libp2p Network key. Default: `true`.

---

<h4><i>bls</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets init [--bls FLAG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets init --bls

  </TabItem>
</Tabs>

Sets the flag indicating whether to generate a BLS key. Default: `true`.

### secrets generate flags

<h4><i>dir</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets generate [--dir DATA_DIRECTORY]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets generate --dir ./example-dir

  </TabItem>
</Tabs>

Sets the directory for the secrets manager configuration file Default: `./secretsManagerConfig.json`

---

<h4><i>type</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets generate [--type TYPE]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets generate --type hashicorp-vault

  </TabItem>
</Tabs>

Specifies the type of the secrets manager [`hashicorp-vault`]. Default: `hashicorp-vault`

---

<h4><i>token</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets generate [--token TOKEN]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets generate --token s.zNrXa9zF9mgrdnClM7PZ19cu

  </TabItem>
</Tabs>

Specifies the access token for the service

---

<h4><i>server-url</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets generate [--server-url SERVER_URL]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets generate --server-url http://127.0.0.1:8200

  </TabItem>
</Tabs>

Specifies the server URL for the service

---

<h4><i>name</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets generate [--name NODE_NAME]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets generate --name node-1

  </TabItem>
</Tabs>

Specifies the name of the node for on-service record keeping. Default: `metabit-chain-node`

---

<h4><i>namespace</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets generate [--namespace NAMESPACE]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets generate --namespace my-namespace

  </TabItem>
</Tabs>

Specifies the namespace used for the Hashicorp Vault secrets manager. Default: `admin`

### secrets output flags

<h4><i>bls</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets output [--bls FLAG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets output --bls

  </TabItem>
</Tabs>

Sets the flag indicating whether to only output the BLS public key. Default: `true`

---

<h4><i>config</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets output [--config SECRETS_CONFIG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets output --config ./secretsManagerConfig.json

  </TabItem>
</Tabs>

Sets the path to the SecretsManager config file. If omitted, the local FS secrets manager is used.

---

<h4><i>data-dir</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets output [--data-dir DATA_DIRECTORY]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets output --data-dir ./example-dir

  </TabItem>
</Tabs>

Sets the directory for the Metabit Chain data if the local FS is used.

---

<h4><i>node-id</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets output [--node-id FLAG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets output --node-id

  </TabItem>
</Tabs>

Sets the flag indicating whether to only output the network node ID. Default: `true`

---

<h4><i>validator</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secrets output [--validator FLAG]

  </TabItem>
  <TabItem value="example" label="Example">

    secrets output --validator

  </TabItem>
</Tabs>

Sets the flag indicating whether to only output the validator address. Default: `true`

---

## Responses

### Status Response

The response object is defined using Protocol Buffers.
````go title="minimal/proto/system.proto"
message ServerStatus {
    int64 network = 1;

    string genesis = 2;

    Block current = 3;

    string p2pAddr = 4;

    message Block {
        int64 number = 1;
        string hash = 2;
    }
}
````

### Monitor Response
````go title="minimal/proto/system.proto"
message BlockchainEvent {
    // The "repeated" keyword indicates an array
    repeated Header added = 1;
    repeated Header removed = 2;

    message Header {
        int64 number = 1;
        string hash = 2;
    }
}
````

## Utilities

### whitelist commands

| **Command**            | **Description**                                                                     |
|------------------------|-------------------------------------------------------------------------------------|
| whitelist show         | Displays whitelist information                     |
| whitelist deployment   | Updates the smart contract deployment whitelist |

<h3> whitelist show </h3>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    whitelist show

  </TabItem>
</Tabs>

Displays whitelist information.

---

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    whitelist show [--chain GENESIS_FILE]

  </TabItem>
  <TabItem value="example" label="Example">

    whitelist show --chain genesis.json

  </TabItem>
</Tabs>

Specifies the genesis file to update. Default: `./genesis.json`.

---

<h3> whitelist deployment </h3>

<h4><i>chain</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    whitelist deployment [--chain GENESIS_FILE]

  </TabItem>
  <TabItem value="example" label="Example">

    whitelist deployment --chain genesis.json

  </TabItem>
</Tabs>

Specifies the genesis file to update. Default: `./genesis.json`.

---

<h4><i>add</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    whitelist deployment [--add ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    whitelist deployment --add 0x5383Cb489FaCa92365Bb6f9f1FB40bD032E6365d

  </TabItem>
</Tabs>

Adds a new address to the contract deployment whitelist. Only the addresses in the contract deployment whitelist can deploy contracts. If empty, any address can execute the contract deployment

---

<h4><i>remove</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    whitelist deployment [--remove ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    whitelist deployment --remove 0x5383Cb489FaCa92365Bb6f9f1FB40bD032E6365d

  </TabItem>
</Tabs>

Removes an address from the contract deployment whitelist. Only the addresses in the contract deployment whitelist can deploy contracts. If empty, any address can execute the contract deployment

---

### backup flags

<h4><i>grpc-address</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    backup [--grpc-address GRPC_ADDRESS]

  </TabItem>
  <TabItem value="example" label="Example">

    backup --grpc-address 127.0.0.1:9632

  </TabItem>
</Tabs>

Address of the gRPC API. Default: `127.0.0.1:9632`.

---

<h4><i>out</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    backup [--out OUT]

  </TabItem>
  <TabItem value="example" label="Example">

    backup --out backup.dat

  </TabItem>
</Tabs>

Path of archive file to save.

---

<h4><i>from</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    from [--from FROM]

  </TabItem>
  <TabItem value="example" label="Example">

    backup --from 0x0

  </TabItem>
</Tabs>

The beginning height of blocks in archive. Default: 0.

---

<h4><i>to</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    to [--to TO]

  </TabItem>
  <TabItem value="example" label="Example">

    backup --to 0x2710

  </TabItem>
</Tabs>

The end height of blocks in archive.

---

## Genesis Template
The genesis file should be used to set the initial state of the blockchain (ex. if some accounts should have a starting balance).

The following *./genesis.json* file is generated:
````json
{
    "name": "example",
    "genesis": {
        "nonce": "0x0000000000000000",
        "gasLimit": "0x0000000000001388",
        "difficulty": "0x0000000000000001",
        "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "coinbase": "0x0000000000000000000000000000000000000000",
        "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000"
    },
    "params": {
        "forks": {},
        "chainID": 100,
        "engine": {
            "pow": {}
        }
    },
    "bootnodes": []
}
````

### Data Directory

When executing the *data-dir* flag, a **test-chain** folder is generated.
The folder structure consists of the following sub-folders:
* **blockchain** - Stores the LevelDB for blockchain objects
* **trie** - Stores the LevelDB for the Merkle tries
* **keystore** - Stores private keys for the client. This includes the libp2p private key and the sealing/validator private key
* **consensus** - Stores any consensus information that the client might need while working

## Resources
* **[Protocol Buffers](https://developers.google.com/protocol-buffers)**
