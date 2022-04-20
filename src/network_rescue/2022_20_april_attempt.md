# 2022 20 April attempt

@Ashiiix  
Modifications in the validator yaml file (manual instructions) use @drawks method first:
1- add the seeds in validator_network.seeds  
2- change the discovery_method (validator_network.discovery_method) to none  
3- remove the entire section 'full_node_networks'  
75426314240 Apr 15 02:29 0L.167.tar.xz*  
git log
commit 412dbdaa832c19792a25d43170452dfda40173ca (HEAD -> rescue-mission, origin/rescue-mission)

@drawks  
`python3 -c 'import yaml;`   
`yaml.safe_load(open(".0L/validator.node.yaml"))'`      
this is a quick command you can use to validate that your validator node config is parsable yaml. I know people often have whitespace indenting problems when pasting into yaml documents

## Example validator.yaml
see validator list in [validator ip google sheet](https://docs.google.com/spreadsheets/d/17Hd0xhIXdNmstLkI4cY5FBm6KrgdgZyWpBV3LK6CN-E/edit#gid=0)
change 
1. ` discovery_method:` to  `discovery_method: none`
2. `seeds: {}` to


```yaml
validator_network:
  max_connection_delay_ms: 60000
  connection_backoff_base: 2
  connectivity_check_interval_ms: 5000
  network_channel_size: 1024
  max_concurrent_network_reqs: 100
  discovery_method: none 
  identity:
    type: from_storage
    backend:
      type: on_disk_storage
      path: /home/0L/.0L/key_store.json
      namespace: 34b5d5e56ec27d954ac5d40b24d11422-oper
    key_name: validator_network
    peer_id_name: owner_account
  listen_address: /ip4/0.0.0.0/tcp/6180
  mutual_authentication: true
  network_address_key_backend:
    type: on_disk_storage
    path: /home/0L/.0L/key_store.json
    namespace: 34b5d5e56ec27d954ac5d40b24d11422-oper
  network_id: validator
  seed_addrs: {}
  seeds: {}
  max_frame_size: 8388608
  enable_proxy_protocol: false
  ping_interval_ms: 1000
  ping_timeout_ms: 10000
  ping_failures_tolerated: 10000
  max_outbound_connections: 100
  max_inbound_connections: 100
  inbound_rate_limit_config: ~
  outbound_rate_limit_config: ~
failpoints: ~
```