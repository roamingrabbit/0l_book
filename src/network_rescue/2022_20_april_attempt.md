# 2022 20 April attempt

### Outcome 

Successfully started a network with the following validators  
`export VALS="4B08C148F5E80962BE1E5755F0D2ED29 1C03E956DD7AFC612E4EFE240C23365D
012338b54ba4625adcc313394d87819c 987be6e871faeedfe255b4305b4c6d02
D96E89E270A5273D94BC8AB7953754F9 D1C9CE9308B0BDC6DC2BA6A7B5DA8C2B"`

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
Seeds example from @Ashiiix
```yaml
  seeds:
    7EC16859C24200D8E074809D252AC740:
      addresses:
        - "/ip4/35.231.138.89/tcp/6180/ln-noise-ik/987f636ef651abc3bc0ad1a33ef2e5841768fde064971333059d84442bb3d576/ln-handshake/0"
      role: "Validator"
    46A7A744B5D33C47F6B20766F8088B10:
      addresses:
        - "/ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0"
      role: "Validator"
    ECAF65ADD1B785B0495E3099F4045EC0:
      addresses:
        - "/ip4/34.145.88.77/tcp/6180/ln-noise-ik/14680097d0ae4d37158ade5c90da4ce43b13c5dbeb918016f0cc8e9830f54f33/ln-handshake/0"
      role: "Validator"
    8186F4D8FDD09DFE02963B0B4C385105:
      addresses:
        - "/ip4/20.39.34.205/tcp/6180/ln-noise-ik/2e7b8c6cf5abff63f88b26bd960e2c586f3723d08c895cc04c5eef3449a3905e/ln-handshake/0"
      role: "Validator"
    4B08C148F5E80962BE1E5755F0D2ED29:
      addresses:
        - "/ip4/65.108.73.53/tcp/6180/ln-noise-ik/33ed842980f68a0a78d2d5d240b062c8cae59ebf58b25fa07022fd93133c457a/ln-handshake/0"
      role: "Validator"
    E264023342B41ACCDBB61A190B6CB2A7:
      addresses:
        - "/ip4/137.184.118.15/tcp/6180/ln-noise-ik/e41c5b51f18d9826ca23136f0edc442d701c82c246ed1f306ece495e763df823/ln-handshake/0"
      role: "Validator"
    1C03E956DD7AFC612E4EFE240C23365D:
      addresses:
        - "/ip4/161.35.228.136/tcp/6180/ln-noise-ik/a08e233ebead3c9467175df8d86a1d9ab46ce0f1c7998bdac59fc58208236837/ln-handshake/0"
      role: "Validator"
    56641E58ABA97FA6B7EA833F83444392:
      addresses:
        - "/ip4/82.165.250.66/tcp/6180/ln-noise-ik/6c3f93028522845daaecf17d2c2a1359473435d9491b593e39a8c839371de03e/ln-handshake/0"
      role: "Validator"
    D1281DE242839FC939745996882C5FC2:
      addresses:
        - "/ip4/172.31.11.23/tcp/6180/ln-noise-ik/e0f25c377b55581bc2c11fd03cb9ae5eba7ef276e32865d98b3e1b7436fc4020/ln-handshake/0"
      role: "Validator"
    012338B54BA4625ADCC313394D87819C:
      addresses:
        - "/ip4/63.229.234.74/tcp/6180/ln-noise-ik/7825869ae4c0cb91bbd8027ce16c64680f84c979320f8921fc76a17c7bec6f32/ln-handshake/0"
      role: "Validator"
    987BE6E871FAEEDFE255B4305B4C6D02:
      addresses:
        - "/ip4/3.12.14.24/tcp/6180/ln-noise-ik/cb7e573123b67b0bb957d23f0d11c65b0b5438815b3750461c3815d507fb5649/ln-handshake/0"
      role: "Validator"
    D96E89E270A5273D94BC8AB7953754F9:
      addresses:
        - "/ip4/65.108.108.82/tcp/6180/ln-noise-ik/b998763ff5e33ec52baad9d3a3f395451202fee3690c8f98a372fa2c67bcca70/ln-handshake/0"
      role: "Validator"
    D1C9CE9308B0BDC6DC2BA6A7B5DA8C2B:
      addresses:
        - "/ip4/34.130.72.87/tcp/6180/ln-noise-ik/6669e2741fe958f94a0a2e4965e7657b904592bb724c3e662d45d091ad473530/ln-handshake/0"
      role: "Validator"
    34B5D5E56EC27D954AC5D40B24D11422:
      addresses:
        - "/ip4/104.197.186.76/tcp/6180/ln-noise-ik/c61044a4544c832bd998e0eded2fa7798a8f59b8219e0c9eef718c8b6f804b2a/ln-handshake/0"
      role: "Validator"
    A2FAB2DF081CD8FEED7F4D6AD2FFF459:
      addresses:
        - "/ip4/176.9.114.29/tcp/6180/ln-noise-ik/863f660ff03a2fdc8ef3e1bf7eaf2f7f127d5bdb709a8c6af3218a09e27a790d/ln-handshake/0"
      role: "Validator"
    9A710919B1A1E67EDA335269C0085C91:
      addresses:
        - "/ip4/24.229.105.9/tcp/6180/ln-noise-ik/3c37c7d6a5122a6b9ef07a11cc40e445874eb0841ae028d6326bf67768cce235/ln-handshake/0"
      role: "Validator"
    B5B5BA58B8E9916FE449D1F989383834:
      addresses:
        - "/ip4/159.223.49.139/tcp/6180/ln-noise-ik/c1954be575981591f2eabd67913c839657ac45a866b15bff40b5d80eb4d82778/ln-handshake/0"
      role: "Validator"

```

## Instructions
Check out release should be at commit `56a0d296bce022ec3c1d96f8b8321099d56ab255`
```console
$ cd libra
$ git fetch && git checkout release-v5.1.0 -f

# make sure you are on the same commit hash
$ git log
commit 56a0d296bce022ec3c1d96f8b8321099d56ab255

# all make command run from libra/language/diem-tools/writeset-transaction-generator dir
$ cd ./language/diem-tools/writeset-transaction-generator
$ make tx
$ make check

# verify that your waypoint it correct, for this session the waypoint needed to be:
# 37235343:44f96bb61f3977f3e1a22abbd21c1f1ad9d6fe3dea3861fcf128cf909e423b22
$ cat ~/.0L/rescue/rescue_waypoint.txt 
7235343:44f96bb61f3977f3e1a22abbd21c1f1ad9d6fe3dea3861fcf128cf909e423b22

# now your are ready for the real deal

# commit your current waypoint? TDOO: Not sure this is really what is being done.
$ make commit

# init your?? TODO: maybe setting the stdlib and validator set?  
$ make init

```

Now you are ready to run your validator node. you need at **least one `seed` set 
in the validator.yam**l (see above)


there are tweo ways to run your validator:
1. `make start` 
2. run `diem-node`  

`make start` will recompile everything, so this will take time, but there aren't 
any changes to diem-node so if you have a running diem-node you are fine to start that
as is.

```
$ diem-node -f ~/.0L/validator.node.yaml >> ~/.0L/logs/validator.log 2>&1
```
or
```console
$ cd ~/libra/language/diem-tools/writeset-transaction-generator
$ make start 
```

## Nibblers log

```console
$ cd ~/libra
$ git fetch && git checkout release-v5.1.0 -f
libra$ cd ./language/diem-tools/writeset-transaction-generator

$ git log
commit 56a0d296bce022ec3c1d96f8b8321099d56ab255

# export the validators that will be in the intitial set, this is important and necessary
# to do before running the subsequent commands (not sure this is true - as it will affect the waypoint?)
$ export VALS="D1281DE242839FC939745996882C5FC2 4B08C148F5E80962BE1E5755F0D2ED29 D96E89E270A5273D94BC8AB7953754F9 34b5d5e56ec27d954ac5d40b24d11422 987be6e871faeedfe255b4305b4c6d02 46A7A744B5D33C47F6B20766F8088B10 E264023342B41ACCDBB61A190B6CB2A7"

$ make tx
Finished dev [unoptimized + debuginfo] target(s) in 3m 37s
Running `target/debug/diem-writeset-generator --db /home/0L/.0L/db --output /home/0L/.0L/rescue/rescue.blob rescue 46A7A744B5D33C47F6B20766F8088B10`
encode stdlib changeset
```

```console
$ make check
[execution/executor/src/db_bootstrapper.rs:138] &next_epoch = 168
[execution/executor/src/db_bootstrapper.rs:139] "epoch" = "epoch"
[execution/executor/src/db_bootstrapper.rs:139] &get_state_epoch(&state_view)? = 168
Waypoint: 37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee

$ cat ~/.0L/rescue/rescue_waypoint.txt
37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee

export VALS="4B08C148F5E80962BE1E5755F0D2ED29 1C03E956DD7AFC612E4EFE240C23365D 
012338b54ba4625adcc313394d87819c 987be6e871faeedfe255b4305b4c6d02 
D96E89E270A5273D94BC8AB7953754F9 D1C9CE9308B0BDC6DC2BA6A7B5DA8C2B"

validator seeds doesn't mean in valdiator set
```
ok same set of vals before 4:43et
```
$ export VALS="D1281DE242839FC939745996882C5FC2 4B08C148F5E80962BE1E5755F0D2ED29 D96E89E270A5273D94BC8AB7953754F9 34b5d5e56ec27d954ac5d40b24d11422 987be6e871faeedfe255b4305b4c6d02 46A7A744B5D33C47F6B20766F8088B10 E264023342B41ACCDBB61A190B6CB2A7"
$ cd ~/libra/language/diem-tools/writeset-transaction-generator
$ make tx
 Finished dev [unoptimized + debuginfo] target(s) in 0.62s
     Running `target/debug/diem-writeset-generator --db /home/0L/.0L/db --output /home/0L/.0L/rescue/rescue.blob rescue 4B08C148F5E80962BE1E5755F0D2ED29 D96E89E270A5273D94BC8AB7953754F9 34b5d5e56ec27d954ac5d40b24d11422 987be6e871faeedfe255b4305b4c6d02 46A7A744B5D33C47F6B20766F8088B10 E264023342B41ACCDBB61A190B6CB2A7 8186f4d8fdd09dfe02963b0b4c385105`
encode stdlib changeset

$ make check
    Finished dev [unoptimized + debuginfo] target(s) in 0.57s
     Running `target/debug/db-bootstrapper /home/0L/.0L/db/ --genesis-txn-file /home/0L/.0L/rescue/rescue.blob`
[execution/executor/src/db_bootstrapper.rs:138] &next_epoch = 168
[execution/executor/src/db_bootstrapper.rs:139] "epoch" = "epoch"
[execution/executor/src/db_bootstrapper.rs:139] &get_state_epoch(&state_view)? = 168
Waypoint: 37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee

$ cat ~/.0L/rescue/rescue_waypoint.txt
37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee 

Wrong waypoint, delete db and untar again...
waypoint should be: 37235343:44f96bb61f3977f3e1a22abbd21c1f1ad9d6fe3dea3861fcf128cf909e423b22

$ cd ~/libra/language/diem-tools/writeset-transaction-generator 

$ make tx
  Finished dev [unoptimized + debuginfo] target(s) in 2.25s
     Running `target/debug/diem-writeset-generator --db /home/0L/.0L/db --output /home/0L/.0L/rescue/rescue.blob rescue 4B08C148F5E80962BE1E5755F0D2ED29 D96E89E270A5273D94BC8AB7953754F9 34b5d5e56ec27d954ac5d40b24d11422 987be6e871faeedfe255b4305b4c6d02 46A7A744B5D33C47F6B20766F8088B10 E264023342B41ACCDBB61A190B6CB2A7 8186f4d8fdd09dfe02963b0b4c385105`
encode stdlib changeset
$ make check
cd /home/0L/libra && cargo r -p db-bootstrapper -- $HOME/.0L/db/ --genesis-txn-file $HOME/.0L/rescue/rescue.blob | grep -oP 'waypoint: \K\w+:\w+' > $HOME/.0L/rescue/rescue_waypoint.txt
    Finished dev [unoptimized + debuginfo] target(s) in 0.57s
     Running `target/debug/db-bootstrapper /home/0L/.0L/db/ --genesis-txn-file /home/0L/.0L/rescue/rescue.blob`
     
$ cat rescue_waypoint.txt
37235343:44f96bb61f3977f3e1a22abbd21c1f1ad9d6fe3dea3861fcf128cf909e423b22


$ make commit
warning: 1 warning emitted

    Finished dev [unoptimized + debuginfo] target(s) in 25.21s
     Running `target/debug/diem-transaction-replay --db /home/0L/.0L/db annotate-account 00000000000000000000000000000000`
make[1]: Leaving directory '/home/0L/libra/language/diem-tools/writeset-transaction-generator'

$ make init
$ make start
canceld out because taking too long just run diem-node
$  RUST_LOG=error diem-node -f ~/.0L/validator.node.yaml >> ~/.0L/logs/validator.log 2>&1
$ tail -f validator.log
2022-04-20T21:25:29.627535Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 8186f4d8 at /ip4/20.39.34.205/tcp/6180/ln-noise-ik/2e7b8c6cf5abff63f88b26bd960e2c586f3723d08c895cc04c5eef3449a3905e/ln-handshake/0: Transport error: Connection refused (os error 111) {"error":"Transport error: Connection refused (os error 111)","network_address":"/ip4/20.39.34.205/tcp/6180/ln-noise-ik/2e7b8c6cf5abff63f88b26bd960e2c586f3723d08c895cc04c5eef3449a3905e/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"8186F4D8FDD09DFE02963B0B4C385105"}
2022-04-20T21:25:36.575411Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 8186f4d8 at /ip4/20.39.34.205/tcp/6180/ln-noise-ik/2e7b8c6cf5abff63f88b26bd960e2c586f3723d08c895cc04c5eef3449a3905e/ln-handshake/0: Transport error: Connection refused (os error 111) {"error":"Transport error: Connection refused (os error 111)","network_address":"/ip4/20.39.34.205/tcp/6180/ln-noise-ik/2e7b8c6cf5abff63f88b26bd960e2c586f3723d08c895cc04c5eef3449a3905e/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"8186F4D8FDD09DFE02963B0B4C385105"}
2022-04-20T21:25:39.604666Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 46a7a744 at /ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0: Transport error: timeout elapsed {"error":"Transport error: timeout elapsed","network_address":"/ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"46A7A744B5D33C47F6B20766F8088B10"}
====================================== 149 ======================================
```
```console
$ export VALS="4B08C148F5E80962BE1E5755F0D2ED29 D96E89E270A5273D94BC8AB7953754F9 34b5d5e56ec27d954ac5d40b24d11422 987be6e871faeedfe255b4305b4c6d02 46A7A744B5D33C47F6B20766F8088B10 E264023342B41ACCDBB61A190B6CB2A7 8186f4d8fdd09dfe02963b0b4c385105"

$ cd ~/libra/language/diem-tools/writeset-transaction-generator 

$ make tx-migrate
...
[move print] 100240
[move print] 100240
[move print] 100240

$ make check
    Finished dev [unoptimized + debuginfo] target(s) in 0.56s
     Running `target/debug/db-bootstrapper /home/0L/.0L/db/ --genesis-txn-file /home/0L/.0L/rescue/rescue.blob`
[execution/executor/src/db_bootstrapper.rs:138] &next_epoch = 169
[execution/executor/src/db_bootstrapper.rs:139] "epoch" = "epoch"
[execution/executor/src/db_bootstrapper.rs:139] &get_state_epoch(&state_view)? = 169
Waypoint:
```
once on the same waypoint: `37235489:b019393e57fdb375143d1d864843362c393ee55d4123bdd2cf0ec7a088a500f2`

**note** if your waypoint is `37235343:6c5ec285db421a510837b7733574b43c984fa73b1f7cc969c1ac10b7bcfba88b` 
make sure you set the `VALS` evn var (see above)
```console/home/0L/
$ cat ~/.0L/rescue/rescue_waypoint.txt
37235489:b019393e57fdb375143d1d864843362c393ee55d4123bdd2cf0ec7a088a500f2

$ make init
$ make start or run diem-node 
2022-04-20T21:42:32.193999Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 8186f4d8 at /ip4/20.39.34.205/tcp/6180/ln-noise-ik/2e7b8c6cf5abff63f88b26bd960e2c586f3723d08c895cc04c5eef3449a3905e/ln-handshake/0: Transport error: Connection refused (os error 111) {"error":"Transport error: Connection refused (os error 111)","network_address":"/ip4/20.39.34.205/tcp/6180/ln-noise-ik/2e7b8c6cf5abff63f88b26bd960e2c586f3723d08c895cc04c5eef3449a3905e/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"8186F4D8FDD09DFE02963B0B4C385105"}
====================================== 121 ======================================
```

## changes
better tools for permission
permission trees / ancestory
makewhole 
voucher info - validators identifying other trusted peers

TODO
1. genesis tx
2. start db again
3. then stop it
4. then another writeset tx for migration
means could start a network, then stop it
someone apply tx 
then shart the snapshot with everyone else

or 

1 person first apply initial writeset tx 
2. create snap share
3. everyone does second writeset tx.


tools will allow future recovery to be done without backup and restor.
Q: what is happening when applying writeset
A: writeset blockchain tx, normally tx need user to sign restricted, with writeset can be vm
can sign as root of blockchain and can do any tx we want.
if root only a certain number of things you can do, in 0L root can't do anythign in runningchain
only certain ops at each block or epoch trigger a small about of tx root acct can do. when blockchain offline
tool to run any function in stdlib as any user. we can also apply migration, e.g. Makewhole, pretty complex
migration to migrate while blockchain running, get auth to change info on people's account, complicated work around, but
since db at rest, write tx assuming roles of certain users.

1. new stdlib: We couldn't jailbreak  
2. had to change validator set.
