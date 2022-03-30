# diem-node

### Modes
* Fullnodes 
* Validator

### Running Diem-node

```console
$ git clone https://github.com/OLSF/libra.git
$ cd libra/diem-node
$ cargo build --release


$ ../target/release/diem-node -help
USAGE:
    diem-node [FLAGS] --config <config>

FLAGS:
    -h, --help            Prints help information
        --random-ports    Enabling random ports for testnet
        --test            Enable a single validator testnet
    -V, --version         Prints version information

OPTIONS:
    -f, --config <config>    Path to NodeConfig
```
**note**: build sizes can be large! Just building diem-node -> 6G debug, or 1.6G release

## Start a local diem-node node
TODO: as validator, fullnode..

```console
$ ../target/release/diem-node --test --random-ports

initializing owner: 4C613C2F4B1E67CA8D98A542EE3F59F5
initializing owner: 4C613C2F4B1E67CA8D98A542EE3F59F5
Completed generating configuration:
	Log file: "/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/2ceeeae60a29b79b3404903c781bbdaa/validator.log"
	Config path: "/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/2ceeeae60a29b79b3404903c781bbdaa/0/node.yaml"
	Diem root key path: "/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/2ceeeae60a29b79b3404903c781bbdaa/mint.key"
	Waypoint: 0:59374e97ac98dcf82638fc5419f7a1e3d640d380b5c2675dda47ebbdfe8047cc
	JSON-RPC endpoint: 0.0.0.0:51534
	FullNode network: /ip4/0.0.0.0/tcp/51542
	ChainId: TESTING

Diem is running, press ctrl-c to exit

====================================== 1 ======================================
====================================== 1 ======================================
====================================== 2 ======================================
0L ==== stdlib upgrade: checking for stdlib upgrade
====================================== 3 ======================================
```

## Submit an RPC call to your local node
see [json-rpc-spec.md](https://github.com/OLSF/libra/blob/main/json-rpc/json-rpc-spec.md)

```console
$ curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"get_currencies","params":[],"id":1}' "http://0.0.0.0:51534/"

{"diem_chain_id":4,"diem_ledger_version":1852,"diem_ledger_timestampusec":1648355046274653,"jsonrpc":"2.0","id":1,"result":[{"code":"GAS","scaling_factor":1000000,"fractional_part":1000,"to_xdx_exchange_rate":1.0,"mint_events_key":"050000000000000000000000000000000000000000000000","burn_events_key":"060000000000000000000000000000000000000000000000","preburn_events_key":"070000000000000000000000000000000000000000000000","cancel_burn_events_key":"080000000000000000000000000000000000000000000000","exchange_rate_update_events_key":"090000000000000000000000000000000000000000000000"}]}
```

