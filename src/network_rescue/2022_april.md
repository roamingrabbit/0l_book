# 2022 April 100 onboard

## What Happened? 
Block production stopped mid of epoch 165 (last block was produced 2022-04-09 at 12:00:34 CEST  / 10:00:34 UTC / 06:00:34 ET). In the subsequent epoch 166, validators were still failing to produce blocks and thus virtually no proofs were submitted.
This triggered a conditional in the 
[on chain move library EpochBoundry.move](https://github.com/OLSF/libra/blob/820ec66f3457fb26a4e24c952407d37f05ce6b1c/language/diem-framework/modules/0L/EpochBoundary.move#L148-L156)  
that contained a bug: instead of keeping the same validator set from the previous epoch, the `top_accounts`, capped at 100 
validators, made it to the next epoch 167. Out of the 100 validators in the new epoch, some were seemingly
not actively maintained and were unknown entities with no means of contacting the operators. 

Attempt 1 (11 April 2022 4pm EST): There was a coordinated restart of the network done during a validator discord call. 
The validators on the call did a synchronized restart of the nodes they controlled and many 
validators set a [cron job to restart their validator every 1 hour](https://github.com/OLSF/libra/blob/validator-autorestart-doc/ol/documentation/node-ops/auto_restart_validators.md). 
It was requested that validator turn off towers and fullnodes
and only run their validators.  
Blocks started to be produced, albeit slower than normal, and occationally block production would be halted.

Next a **[detailed plan](https://hackmd.io/8pNAlRk-TpypCgQVQGWHzw)** was outlined as to what next steps could be taken to recover the network.
> Plan A: Organize a Synchronous start with the 100 validators in the network.

> Plan B: Issue a manual writeset transaction to overwrite the validator set to approx 10 validators, with no state change. (soft fork)

> Plan C: Scorched earth state dump and overwrite validator set (approx 10), preserving only balances, tower-state, and validator configs.

Eagle Network 15 April 2022 launched as a test network for a reconfigured validator set. 

## Links
- [2022 Apirl 13th POA / Call to action](https://hackmd.io/8pNAlRk-TpypCgQVQGWHzw)  
- [epoch 168 validators](https://docs.google.com/spreadsheets/d/1T8-TzSQvICk3Q49ooGUxTACeE4_BZRnnBdxSIM-67Cw/edit#gid=0)  
- [11th April validator coordinated restart](https://docs.google.com/spreadsheets/d/1QRal4-LLuDZIiLyMsMV_2_nteuNc4avuykoPWg6Od_g/edit#gid=1546165814)  
- [fullnode seed playlist](https://raw.githubusercontent.com/OLSF/seed-peers/main/fullnode_seed_playlist.json)
- [epoch-archive](https://github.com/OLSF/epoch-archive/blob/main/Makefile)
- [disaster-recovery doc - update db, update stdlib](https://github.com/OLSF/libra/blob/rescue-mission/ol/documentation/network-upgrades/disaster-recovery.md)

## Related Github Issues 
- [Only increase validator sets by at most 25% between epochs 1066](https://github.com/OLSF/libra/issues/1066) 

## Rescue Mission Branch and Docs
- [Plan B - Manual Overrides to State](https://github.com/OLSF/libra/blob/rescue-mission/ol/documentation/network-upgrades/disaster-recovery.md)
- [writeset-transaction-generator Makefile](https://github.com/OLSF/libra/blob/rescue-mission/language/diem-tools/writeset-transaction-generator/Makefile)
- [Network Recovery Tools](https://github.com/OLSF/libra/pull/1071)

## Debug Commands / endpoints
- [set cron job to restart validators every hour](https://github.com/OLSF/libra/blob/validator-autorestart-doc/ol/documentation/node-ops/auto_restart_validators.md)
- web server: obtain validator's IPs via the web monitor -> validators -> click on `(i)` icon next to the validator IP, check if reachable on port.
```console
$ nc -zv $IP 6180
```
- web server: vital endpoint http://$IP:3030/vitals
- [`backup-cli`](https://github.com/OLSF/epoch-archive#backup-cli):
   1. `db-backup` tool [DiemDB Backup](https://github.com/diem/diem/blob/main/specifications/db_backup/spec.md)
   2. `db-restore` tool  
- `db-bootstrapper`   
   apply the writeset to the database `cargo r -p db-bootstrapper -- ~/.0L/db/ --genesis-txn-file ~/.0L/restore/rescue.blob` 
- `diem-transaction-replay`: inspect state of db.  
   export the 0x0 state to file for easy viewing:   
  `cargo r -p diem-transaction-replay -- --db ~/.0L/db annotate-account 00000000000000000000000000000000 > ~/.0L/dump-a
  sha256sum ~/.0L/dump-a`
- ` diem-writeset-generator`: create tx binaries and save the files (files applied later, e.g. via `db-bootstrapper`)
- try reconfig event: `cargo r -p diem-writeset-generator -- --output ~/.0L/restore/rescue.blob reconfig ~/.0L/db`
- try stdlib update: `cargo r -p diem-writeset-generator -- --output ~/.0L/restore/rescue.blob update-stdlib ~/.0L/db`
- `ol/genesis-tool`
- [`db-bootstrapper`](https://github.com/OLSF/libra/blob/main/execution/db-bootstrapper/src/bin/db-bootstrapper.rs): 
  typically used to create genesis file, can be used to apply writeset to a database at rest (halted network).

## Relevant code
- [BUG: Validator failover not implemented to spec](https://github.com/OLSF/libra/issues/1063)  
- [Epoch Boundry Val Selection](https://github.com/OLSF/libra/blob/820ec66f3457fb26a4e24c952407d37f05ce6b1c/language/diem-framework/modules/0L/EpochBoundary.move#L148-L156)  
- [genesis tool: Fork Genesis](https://github.com/OLSF/libra/blob/0b2f2901616bdf243151367d8e31f966d0280c1f/ol/genesis-tools/src/fork_genesis.rs)  
- [genesis tool: process snapshot](https://github.com/OLSF/libra/blob/4d4a60f5dfe33b8121d97e46c67f77e6fe28b745/ol/genesis-tools/src/process_snapshot.rs)

- [PR Network Recovery Tools](https://github.com/OLSF/libra/pull/1071)

## Backup / Snapshot Information 
https://github.com/OLSF/epoch-archive/blob/main/165/transaction_37230877-.2066/transaction.manifest
> There are 3 different components to a backup so that a db can be "bootstrapped" and understandable by the diem-node .   
> Epoch is meta information on the Epoch.   
> State Snapshot is the state of the blockchain.  
> Transactions are a history of txs.  
> To bootstrap a working DB you need at least 1 tx. That's why we only put one for the purposes of epoch-archive.

[epoch-archive README.md](https://github.com/OLSF/epoch-archive)

>Backups are a way of bootstrapping the DB. There are 3 types of point-in-time backups:
>
>Epoch Ending  
Transactions  
State Snapshot  
**All three types of backups are needed to restore and bootstrap a database.**

steps taken from [epoch-archive/MAKEFILE](https://github.com/OLSF/epoch-archive/blob/main/Makefile#L74)  
build backup-cli:   
**note** your SOURCE_PATH should be set to your libra project dir. 
```console
$ export SOURCE_PATH=~/libra
$ cd $SOURCE_PATH
$ cargo build -p backup-cli --release
$ cp -f ${SOURCE_PATH}/target/release/db-restore /usr/local/bin/db-restore
$ cp -f ${SOURCE_PATH}/target/release/db-backup /usr/local/bin/db-backup
```
### Snapshot issue
@Abed
```
2022-04-16T14:07:36.417448Z [main] INFO storage/backup/backup-cli/src/backup_types/state_snapshot/backup.rs:58 State snapshot backup started, for version 30189516.
2022-04-16T14:07:36.424378Z [main] ERROR storage/backup/backup-cli/src/utils/error_notes.rs:14 Error raised, see notes. {"error":"request or response body error: error reading a body from connection: unexpected EOF during chunk size line","notes":"\"\""}
2022-04-16T14:07:36.425423Z [main] ERROR storage/backup/backup-cli/src/bin/db-backup.rs:130 main_impl() failed: State snapshot backup failed: request or response body error: error reading a body from connection: unexpected EOF during chunk size line
Error: State snapshot backup failed: request or response body error: error reading a body from connection: unexpected EOF during chunk size line
```
@OD
I think it's because your state has be "pruned"
In node.yaml there is a prune_window field measured in blocks. So your prune window is smaller than the length of an 
epoch. So the db-tool can't find anything beyond
node/fullnode.yaml
```yaml
...
storage:
address: "127.0.0.1:6666"
backup_service_address: "127.0.0.1:6186"
dir: db
grpc_max_receive_len: 100000000
prune_window: 20000
timeout_ms: 30000
...
```

### Hot Stepper Uppers

@Od - main debugging, code diving, solution propositions  
@gnudrew25 - db dump https://home.gouin.io:5443/0L.167.tar.xz   
71G  0L.167.tar.xz
extracted
70G  	./db/diemdb
753M	./db/consensusdb

@shashank @jamesm - move code  
@Ping | ping.pub - tooling for flashing the stdlib  
@Barmaley  
@Adal - modifiying web app to expose ports  
@Abed - working with backup / snapshots
@Daniyal
@drawks

### Lessons Learned
* Getting 100 validator to coordinate is hard.
* No great way to contact validators. Validator contact info could be required in config? Maybe discord name, email or preferred contact.
* Validators that are not active but have accumulated high voting power will potentially kick active validator out of the proposed validator set. 
* Full network archive 70G

## Root Cause Analysis
What could be seen in the logs is that different block proposals existed at the same time. Usually the proposer election algorithm should   chose deterministically one validator as block proposer for the next round and thus only one proposal should exist at a time. Maybe this is the cause, why no consensus could be found: with several proposals it is even more difficult to get a 2/3 majority on one proposal. 

Why several block proposal exist simultaneously is open. Could be due to different config settings of validator nodes in the "consensus" section of validator.node.yaml.


## TODOs (this will be updated until block morale improves)
- [ ] We need a way to get a snapshot of an exact block height. See some info here: https://github.com/OLSF/epoch-archive
https://github.com/OLSF/epoch-archive
Correct failover issue in Move https://github.com/OLSF/libra/pull/1069/ @jamesm   
- [ ]  Find db-backup db-restore sequence to share an archive between validators (volunteers?)
- [ ]  Code rust tools for write set generation @0D | 0o-de-lally  
- [ ]  Code writeset for incrementing timestamp @Ping | ping.pub  
- [ ]  Debug MoveVM cache not being invalidated @shb  
- [ ]  Test block production in Eagle network @0D | 0o-de-lally  
- [ ]  Test tower submission on Eagle @0D | 0o-de-lally  
- [ ]  (Maybe) Change seat rotation algo  https://github.com/OLSF/libra/issues/1066 @shashank @keerthi   
