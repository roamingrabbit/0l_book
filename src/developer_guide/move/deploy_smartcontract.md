# Deploying Smart Contracts

## Move Modules
> Module is a set of functions and types packed together which the developer publishes under his address.

[see move book](https://move-book.com/syntax-basics/module.html?highlight=Unbound,module,alias#module-and-import)

## Move Scripts

## Deploying Move Modules to local testnet 
[see deploy_move_modules_using_diem_testnet](https://github.com/OLSF/libra/blob/main/ol/documentation/core-devs/deploy_move_modules_using_diem_testnet.md)

```console
$ ./diem-node --test --random port

Entering test mode, this should never be used in production!
[config/management/genesis/src/storage_helper.rs:218] "swarm 3" = "swarm 3"
[config/management/genesis/src/storage_helper.rs:218] 
&user = "talent sunset lizard pill fame nuclear spy noodle basket okay critic grow sleep legend hurry pitch blanket clerk impose rough degree sock insane purse"
[config/management/src/validator_config.rs:72] 
&validator_address = /ip4/0.0.0.0/tcp/63818/ln-noise-ik/87b87096e8a7aec05ba62f5362acd1047fe6bbf0a480bf956a9b76e6b8a23103/ln-handshake/0
[config/management/src/validator_config.rs:89] 
&fullnode_address = /ip4/0.0.0.0/tcp/63820/ln-noise-ik/1469513dfddeeb0a11f3cc54f8cae323cbd5b129ec2cf3ed63e11103984e7d3d/ln-handshake/0
initializing owner: 4C613C2F4B1E67CA8D98A542EE3F59F5
initializing owner: 4C613C2F4B1E67CA8D98A542EE3F59F5
Completed generating configuration:
	Log file: "/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/e520ce657a3e49e131d305db60cff0a7/validator.log"
	Config path: "/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/e520ce657a3e49e131d305db60cff0a7/0/node.yaml"
	Diem root key path: "/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/e520ce657a3e49e131d305db60cff0a7/mint.key"
	Waypoint: 0:081599e48facd7709d2ce207db27df39cb6abd795c7c20e7ca5e97b84b6f4548
	JSON-RPC endpoint: 0.0.0.0:63812
	FullNode network: /ip4/0.0.0.0/tcp/63820
	ChainId: TESTING

Diem is running, press ctrl-c to exit

```

#### Start CLI

To run the CLI you need to pass the WAYPOINT, JSON-RPC, ChainId, ROOT_KEY (path), for the running testnet:

```
&user = "talent sunset lizard pill fame nuclear spy noodle basket okay critic grow sleep legend hurry pitch blanket clerk 
impose rough degree sock insane purse"

Diem root key path: "/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/e520ce657a3e49e131d305db60cff0a7/mint.key"

Waypoint: 0:081599e48facd7709d2ce207db27df39cb6abd795c7c20e7ca5e97b84b6f4548

JSON-RPC endpoint: 0.0.0.0:63812

ChainId: TESTING
```

We will export these variable in the same terminal session which we will be running the CLI.
```console

$ export ROOT_KEY="/private/var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/e520ce657a3e49e131d305db60cff0a7/mint.key"
$ export CHAINID="TESTING"
$ export WAYPOINT="0:081599e48facd7709d2ce207db27df39cb6abd795c7c20e7ca5e97b84b6f4548"
$ export JSON-RPC_ENDPOINT="http://0.0.0.0:63812"

```

Now we can run the CLI command, passing in the variables from our running testnet.
You will need your mneumonic for this.
```console
// get the values from above, e.g. ChainId: TESTING, JSON-RPC endpoint  
$ cargo run -p cli -- -c $CHAINID -m $ROOT_KEY -u $JSON_RPC_ENDPOINT --waypoint $WAYPOINT 

Enter your 0L mnemonic:
🔑
length: 6
Wallet recovered and the first 6 child accounts were derived
#0 address 4c613c2f4b1e67ca8d98a542ee3f59f5
#1 address 41db5082582e413725159a43b17c05c0
#2 address f185398445f13d4b01d53d1b07281e68
#3 address c46f39c1461c1bc83c2d2c60625af787
#4 address 64f0f978cc23d5d36d1f5125eec307ef
#5 address 828d998ffc9f45bbca8e4da5c85323f9
Connected to validator at: http://127.0.0.1:63812, latest version = 404, timestamp = 2022-03-29 16:37:35.754821 UTC
usage: <command> <args>

Use the following commands:

account | a
	Account operations
query | q
	Query operations
transfer | transferb | t | tb
	<sender_account_address>|<sender_account_ref_id> <receiver_account_address>|<receiver_account_ref_id> 
	<number_of_coins> <currency_code> [gas_unit_price_in_micro_diems (default=0)] [max_gas_amount_in_micro_diems 
	(default 400_000)] Suffix 'b' is for blocking.
	Transfer coins from one account to another.
info | i
	Print cli config and client internal information
node | n
	Get state of validators, miners.
oracle | o
	Oracle related commands
dev | d
	Local Move development
help | h
	Prints this help
quit | q!
	Exit this client


Please, input commands:

diem%
```

Create accounts using from the CLI REPL
```console
diem% account create
>> Creating/retrieving next local account from wallet
Created/retrieved local account #6 address 7acc85d4e364dd4e6bbb752265ef7de9
```

Working with move `dev` command
```console
diem% dev --help

usage: dev <arg>

Use the following args for this command:

compile | c <sender_account_address>|<sender_account_ref_id> <file_path> <dependency_source_files...>
	Compile Move program
publish | p <sender_account_address>|<sender_account_ref_id> <compiled_module_path>
	Publish Move module on-chain
execute | e <sender_account_address>|<sender_account_ref_id> <compiled_module_path> [parameters]
	Execute custom Move script
upgrade_stdlib | u
	Upgrade the move stdlib used for the blockchain
gen_waypoint | g
	Generate a waypoint for the latest epoch change LedgerInfo
change_diem_version | v <new_diem_version>
	Change the diem_version stored on chain
enable_custom_script | s
	Allow executing arbitrary script in the network. This disables script hash verification.
submit_writeset | ws <path_to_writeset>
	Submit a WriteSet with local diem root account. Path should be a bcs serialized TransactionPayload.
noop | n
	Calls demo_e2e tx script, for testing purposes
```

#### Compile Move Module
`dev compile` is the command we want to compile our `.move` source file to a binary.  
`compile | c <sender_account_address>|<sender_account_ref_id> <file_path> <dependency_source_files...>`  

The dependencies we need are in the `move-stdlib/modules` folder, use the fullpath.

```console
diem% dev compile <FULL_PATH>/PersistenceDemo.move <FULL_PATH_TO_LIBRA_PROJ>/libra/language/move-stdlib/modules
  
    Finished dev [unoptimized + debuginfo] target(s) in 0.48s
     Running `target/debug/move-build <FULL_PATH>/PersistenceDemo.move -o /var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/d27846fb3466d7745dfa6a3626192cd2 -d <FULL_PATH_TO_LIBRA_PROJ>/libra/language/move-stdlib/modules`
Successfully compiled a program at:
  /var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/d27846fb3466d7745dfa6a3626192cd2/modules/0_PersistenceDemo.mv
```
#### Deploy / Publish Move Module
Now you can deploy the module to the testnet
`publish | p <sender_account_address>|<sender_account_ref_id> <compiled_module_path>
Publish Move module on-chain`

```console
diem% dev publish 4C613C2F4B1E67CA8D98A542EE3F59F5 /var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/d27846fb3466d7745dfa6a3626192cd2/modules/0_PersistenceDemo.mv
.....................................................................................................................................................................................................................................................
Successfully published module
```
