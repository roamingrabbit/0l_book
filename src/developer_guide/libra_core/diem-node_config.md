# diem-node config

## diem-node files

```console
$ cd ~.0L/
$ ls

0L.toml                 key_store.json          account.json    
genesis.blob            genesis_waypoint.txt    validator.node.yaml
fullnode.node.yaml      monitor_cache.json       vdf_proofs      
web-monitor             restore                  db

$ ls db
consensusdb  diemdb
```
### 0L.toml
```toml
[workspace]
node_home = "~/.0L/"
block_dir = "vdf_proofs"
db_path = "~/.0L/db"

[profile]
account = "12345678901234567890123456789012"
auth_key = "abcabcabcabcabcabcaabcabcabcabcabcabcbcabcabcabcabcabcabcabcabc"
statement = "Fun statement to start!"
## Public ip of node
ip = "1.2.3.4"
default_node = "http://localhost:8080/"
upstream_nodes = ["http://34.145.88.77:8080/","http://159.223.49.139:8080", "http://138.197.59.9:8080/", "http://35.231.138.89:8080/"]
#upstream_nodes = ["http://34.145.88.77:8080/"]

[chain_info]
chain_id = "1"
## The epoch that you are starting in
base_epoch = 155 
base_waypoint = "1234567:bbbbbbbbbbbaaaaaaaaaaaaaaaaabbbbbbbbbbbbbaaaaaaaaaaabbbbbbbbbbb"
[tx_configs.baseline_cost]
max_gas_unit_for_tx = 10000
coin_price_per_unit = 1
user_tx_timeout = 5000

[tx_configs.critical_txs_cost]
max_gas_unit_for_tx = 1000000
coin_price_per_unit = 1
user_tx_timeout = 5000

[tx_configs.management_txs_cost]
max_gas_unit_for_tx = 100000
coin_price_per_unit = 1
user_tx_timeout = 5000

[tx_configs.miner_txs_cost]
max_gas_unit_for_tx = 10000
coin_price_per_unit = 1
user_tx_timeout = 5000

[tx_configs.cheap_txs_cost]
max_gas_unit_for_tx = 1000
coin_price_per_unit = 1
user_tx_timeout = 5000
```