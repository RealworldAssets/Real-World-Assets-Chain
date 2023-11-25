## Real World Assets Chain

The goal of the Real World Assets Chain is to bring programmability and interoperability to the RWA beacon chain. In order to embrace the existing popular community and advanced technologies, staying compatible with all existing smart contracts and ethereum tools on ethereum will bring huge benefits. And to implement this goal, the easiest solution is to develop based on the go-ethereum fork, because we have a lot of respect for the great work of ethereum.

Real World Assets Chain started development based on the go-ethereum fork. Therefore, you may see many tools, binaries and documentation based on ethereum, such as the name "geth".

[![API Reference](
https://camo.githubusercontent.com/915b7be44ada53c290eb157634330494ebe3e30a/68747470733a2f2f676f646f632e6f72672f6769746875622e636f6d2f676f6c616e672f6764646f3f7374617475732e737667
)](https://pkg.go.dev/github.com/ethereum/go-ethereum?tab=doc)
[![Discord](https://img.shields.io/badge/discord-join%20chat-blue.svg)]()

But starting from the EVM-compatible benchmark, Real World Assets Chain introduces a system of 21 validators with Proof of Stake (PoSA) consensus, which can support shorter block production times and lower fees. The candidate validator with the most binding pledge will become the validator and generate the block. Double sign detection and other cut logic guarantee security, stability and chain finality.

Cross-chain transmissions and other communications are made possible thanks to native support for interoperability. Repeater and on-chain contracts were developed to support this. The RWA Beacon Chain DEX remains a fluid venue for the exchange of assets between two on-chains. This dual-chain architecture is ideal for users to take advantage of fast transactions on one side and build decentralization applications on the other. The **Real World Assets Chain** will be:

- **Self-sovereign blockchain**: providing security through elected validators.
- **EVM Compatible**: Supports all existing ethereum tools as well as faster final deterministic and cheaper transaction fees.
- **Interoperability**: Comes with efficient native dual-chain communication; optimized for scaling high-performance dApps that require a fast, smooth user experience.
- **Distribution through on-chain governance**: Proof of Stake brings decentralization and community participants. As a native token, RWAs will act as fuel and staking tokens for smart contract execution.

More details in [White Paper]().

## Key features

### Proof of Staked Authority 
Although Proof of Work (PoW) has been recognized as a practical mechanism for implementing decentralization networks, it is not environmentally friendly and also requires a large number of participants to maintain security.

Proof of Authority (PoA) provides some defense against 51% attacks, increasing efficiency and tolerance for certain levels of Byzantine players (malicious or hacker attacks). At the same time, the PoA protocol is most criticized for not being decentralized like PoW because validators (i.e. nodes that take turns producing blocks) have all permissions and are vulnerable to corruption and security attacks.

Other blockchains, such as EOS and Cosmos, have introduced different types of proof-of-ownership of stock (DPoS) to allow token holders to vote and choose a set of validators. It increases decentralization and facilitates community governance.

In order to combine DPoS and PoA to reach consensus, Real World Assets Chain implements a new consensus engine called Parlia, which:

1. Blocks are generated by a limited set of validators.
2. Verifiers take turns generating blocks in PoA, similar to ethereum's Clique consensus engine.
3. The election and exit of the validator set is based on the RWA beacon on-chain pledge-based governance.
4. Changes to the validator set are relayed through a cross-chain communication mechanism.
5. The Parlia consensus engine will interact with a set of [system contracts]() to implement functions such as active level reduction, revenue distribution, and validator set updates.


## Native Token

RWA will run on RWA smart on-chain just like ETH runs on ethereum, so it is the same as native tokenBSC. This means, RWA will be used for:

1. Paid `gas` deploys or calls smart contracts on the Real World Assets Chain

## Building the source

Many of the below are the same as or similar to go-ethereum.

For prerequisites and detailed build instructions please read the [Installation Instructions](https://geth.ethereum.org/docs/getting-started/installing-geth).

Building `geth` requires both a Go (version 1.19 or later) and a C compiler (GCC 5 or higher). You can install
them using your favourite package manager. Once the dependencies are installed, run

```shell
make geth
```

or, to build the full suite of utilities:

```shell
make all
```

If you get such error when running the node with self built binary:
```shell
Caught SIGILL in blst_cgo_init, consult <blst>/bindinds/go/README.md.
```
please try to add the following environment variables and build again:
```shell
export CGO_CFLAGS="-O -D__BLST_PORTABLE__" 
export CGO_CFLAGS_ALLOW="-O -D__BLST_PORTABLE__"
```

## Executables

The RWA project comes with several wrappers/executables found in the `cmd`
directory.

|  Command   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| :--------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`geth`** | Main BNB Smart Chain client binary. It is the entry point into the RWA network (main-, test- or private net), capable of running as a full node (default), archive node (retaining all historical state) or a light node (retrieving data live). It has the same and more RPC and other interface as go-ethereum and can be used by other processes as a gateway into the RWA network via JSON RPC endpoints exposed on top of HTTP, WebSocket and/or IPC transports. `geth --help` and the [CLI page](https://geth.ethereum.org/docs/interface/command-line-options) for command line options. |
|   `clef`   | Stand-alone signing tool, which can be used as a backend signer for `geth`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|  `devp2p`  | Utilities to interact with nodes on the networking layer, without running a full blockchain.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|  `abigen`  | Source code generator to convert Ethereum contract definitions into easy to use, compile-time type-safe Go packages. It operates on plain [Ethereum contract ABIs](https://docs.soliditylang.org/en/develop/abi-spec.html) with expanded functionality if the contract bytecode is also available. However, it also accepts Solidity source files, making development much more streamlined. Please see our [Native DApps](https://geth.ethereum.org/docs/dapp/native-bindings) page for details.                                                                                               |
| `bootnode` | Stripped down version of our Ethereum client implementation that only takes part in the network node discovery protocol, but does not run any of the higher level application protocols. It can be used as a lightweight bootstrap node to aid in finding peers in private networks.                                                                                                                                                                                                                                                                                                            |
|   `evm`    | Developer utility version of the EVM (Ethereum Virtual Machine) that is capable of running bytecode snippets within a configurable environment and execution mode. Its purpose is to allow isolated, fine-grained debugging of EVM opcodes (e.g. `evm --code 60ff60ff --debug run`).                                                                                                                                                                                                                                                                                                            |
| `rlpdump`  | Developer utility tool to convert binary RLP ([Recursive Length Prefix](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp)) dumps (data encoding used by the Ethereum protocol both network as well as consensus wise) to user-friendlier hierarchical representation (e.g. `rlpdump --hex CE0183FFFFFFC4C304050583616263`).                                                                                                                                                                                                                                                                                 |

## Running `geth`

Going through all the possible command line flags is out of scope here (please consult our
[CLI Wiki page](https://geth.ethereum.org/docs/fundamentals/command-line-options)),
but we've enumerated a few common parameter combos to get you up to speed quickly
on how you can run your own `geth` instance.

### Hardware Requirements

The hardware must meet certain requirements to run a full node on mainnet:
- VPS running recent versions of Mac OS X, Linux, or Windows.
- IMPORTANT 2.5 TB(May 2023) of free disk space, solid-state drive(SSD), gp3, 8k IOPS, 250 MB/S throughput, read latency <1ms. (if node is started with snap sync, it will need NVMe SSD)
- 16 cores of CPU and 64 GB of memory (RAM)
- Suggest m5zn.3xlarge instance type on AWS, c2-standard-16 on Google cloud.
- A broadband Internet connection with upload/download speeds of 5 MB/S

The requirement for testnet:
- VPS running recent versions of Mac OS X, Linux, or Windows.
- 500G of storage for testnet.
- 4 cores of CPU and 8 gigabytes of memory (RAM).

### Configuration

As an alternative to passing the numerous flags to the `geth` binary, you can also pass a
configuration file via:

```shell
$ geth --config /path/to/your_config.toml
```

To get an idea of how the file should look like you can use the `dumpconfig` subcommand to
export your existing configuration:

```shell
$ geth --your-favourite-flags dumpconfig
```

### Programmatically interfacing `geth` nodes

As a developer, sooner rather than later you'll want to start interacting with `geth` and the
RWA network via your own programs and not manually through the console. To aid
this, `geth` has built-in support for a JSON-RPC based APIs ([standard APIs](https://ethereum.github.io/execution-apis/api-documentation/)
and [`geth` specific APIs](https://geth.ethereum.org/docs/interacting-with-geth/rpc)).
These can be exposed via HTTP, WebSockets and IPC (UNIX sockets on UNIX based
platforms, and named pipes on Windows).

The IPC interface is enabled by default and exposes all the APIs supported by `geth`,
whereas the HTTP and WS interfaces need to manually be enabled and only expose a
subset of APIs due to security reasons. These can be turned on/off and configured as
you'd expect.

HTTP based JSON-RPC API options:

* `--http` Enable the HTTP-RPC server
* `--http.addr` HTTP-RPC server listening interface (default: `localhost`)
* `--http.port` HTTP-RPC server listening port (default: `8545`)
* `--http.api` API's offered over the HTTP-RPC interface (default: `eth,net,web3`)
* `--http.corsdomain` Comma separated list of domains from which to accept cross origin requests (browser enforced)
* `--ws` Enable the WS-RPC server
* `--ws.addr` WS-RPC server listening interface (default: `localhost`)
* `--ws.port` WS-RPC server listening port (default: `8546`)
* `--ws.api` API's offered over the WS-RPC interface (default: `eth,net,web3`)
* `--ws.origins` Origins from which to accept WebSocket requests
* `--ipcdisable` Disable the IPC-RPC server
* `--ipcapi` API's offered over the IPC-RPC interface (default: `admin,debug,eth,miner,net,personal,txpool,web3`)
* `--ipcpath` Filename for IPC socket/pipe within the datadir (explicit paths escape it)

You'll need to use your own programming environments' capabilities (libraries, tools, etc) to
connect via HTTP, WS or IPC to a `geth` node configured with the above flags and you'll
need to speak [JSON-RPC](https://www.jsonrpc.org/specification) on all transports. You
can reuse the same connection for multiple requests!

**Note: Please understand the security implications of opening up an HTTP/WS based
transport before doing so! Hackers on the internet are actively trying to subvert
RWA nodes with exposed APIs! Further, all browser tabs can access locally
running web servers, so malicious web pages could try to subvert locally available
APIs!**



## License

The RWA library (i.e. all code outside of the `cmd` directory) is licensed under the
[GNU Lesser General Public License v3.0](https://www.gnu.org/licenses/lgpl-3.0.en.html),
also included in our repository in the `COPYING.LESSER` file.

The RWA binaries (i.e. all code inside of the `cmd` directory) is licensed under the
[GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html), also
included in our repository in the `COPYING` file.