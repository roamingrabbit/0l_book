# 2022 19 April Attempt

Attempt to start the eagle fork at 6pm ET 

### Required
* Gnudrews' backup database installed as /db (70G)  
  @Barmaley —  @gnudrew25 db snapshot to this public URL: [https://storage.googleapis.com/0l167/0L.167.tar.xz](https://storage.googleapis.com/0l167/0L.167.tar.xz)
              **This db will be required for the rescue effort.**

### Validators
1. @OD
2. Abed `37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee`
3. Adal
4. Ashiiix
5. projecttent `37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee`
6. Daniyal `37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee`
7. drawks `37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee`
8. misko9
9. nibbler `waypoint 37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee`
10. ricoflan
11. shashank
12. svanakin `37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee`
13. Wade|TPT `37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee`
14. thenateway `37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee
15. gnudrew25 

### @nibbler's attempt   
Attempting to bring up validator on a new server
1. copied relevant config files from running validator to a new box
```
0L.toml  account.json  fullnode.node.yaml  genesis.blob  genesis_waypoint.txt    
key_store.json  validator.node.yaml  vdf_proofs
```
2. downloaded Gnudrews' backup database to a mounted dir `/mnt/disks/disk2/netrecover/db/`
and made a symlink to the mounted from the .0l home dir `ln -s /mnt/disks/disk2/netrecover/db/ ~/.0L`
3. updated paths in the config files to match new home dir.

TODO: when ready will reassign the IP associated with the current validator to the new validator box
`104.197.186.76` and hope it all works...
4. reassigned ip, validator came up with db snapshot.
5. made it through steps `make check` 

### Need
* account address
* network network
* shared `validator.node.yaml` share set of seeds.
to get info for `validator.yaml`
```console
$ ol whoami
```
1. use makefile that automats command line, 
2. create a writeset on db at rest  
3. commit it to new db then new start.
4. new start: updated move lib, change validator set, 167 to rescue validators
5. db is changed, but at rest
6. turn on node, will fail immediately.
7. all validators in rescue mission can find each other, then should start producing blocks.

## Steps 
1. check out release-rescue-mission branch 
```console
$ git checkout release-rescue-mission -f
$ make tx
 Finished dev [unoptimized + debuginfo] target(s) in 3m 53s
     Running `target/debug/diem-writeset-generator --db /home/0L/.0L/db --output /home/0L/.0L/rescue/rescue.blob rescue ECAF65ADD1B785B0495E3099F4045EC0`
encode stdlib changeset

```
2. after it finishes run `make check`
```
$ make check 

cat: /home/0L/.0L/rescue_waypoint.txt: No such file or directory
cd /home/0L/libra && cargo r -p db-bootstrapper -- $HOME/.0L/db/ --genesis-txn-file $HOME/.0L/rescue/rescue.blob | grep -oP 'waypoint: \K\w+:\w+' > $HOME/.0L/rescue/rescue_waypoint.txt

```
* potential issue `make check` `too many open files` 
```console
    Running `target/debug/db-bootstrapper /home/0L/.0L/db/ --genesis-txn-file /home/0L/.0L/rescue/rescue.blob`
Error: Failed to open DB.

Caused by:
    IO error: While open a file for random read: /home/0L/.0L/db/diemdb/2046133.sst: Too many open files
make: *** [Makefile:60: check] Error 1
```
#### **solution** Too many open files inc ulimit `$ ulimit -n 500000`
```
# increase file descriptors
ulimit -n 500000
# check that they have been increased
ulimit -n
500000
```
or edit the `/etc/security/limits.conf` file to make this change persistent across sessions:
```
sudo vim /etc/security/limits.conf`
```
append to the end of the `limits.conf`. replace `yourusername` with the output from `whoami`.
``` 
yourusername soft    nproc          500000 
yourusername soft    nproc          500000
yourusername hard    nproc          500000
yourusername soft    nofile         500000
```

**success should look like**
```console
Running `target/debug/db-bootstrapper /home/0L/.0L/db/ --genesis-txn-file /home/0L/.0L/rescue/rescue.blob`
[execution/executor/src/db_bootstrapper.rs:138] &next_epoch = 168
[execution/executor/src/db_bootstrapper.rs:139] "epoch" = "epoch"
[execution/executor/src/db_bootstrapper.rs:139] &get_state_epoch(&state_view)? = 168
Waypoint:
```
3. check in `.0L/rescue/` look for waypoint
```console
$ cd ~/.0L/rescue/ 
rescue_waypoint.txt`
$ cat rescue_waypoint.txt
37235343:8d0ccb390df0044a6b69da45c0f4cdd2d78a1cdc3b90b05172190f6c06221dee
```


## Need Everyone's Validator info `ol whoami`
[google sheet](https://docs.google.com/spreadsheets/d/17Hd0xhIXdNmstLkI4cY5FBm6KrgdgZyWpBV3LK6CN-E/edit#gid=0)


@nibbler
```console
$ ol whoami

0L ACCOUNT

address: 34B5D5E56EC27D954AC5D40B24D11422
...
----- noise protocol addresses -----

Validator (encrypted) address on VALIDATOR network

/ip4/104.197.186.76/tcp/6180/ln-noise-ik/c61044a4544c832bd998e0eded2fa7798a8f59b8219e0c9eef718c8b6f804b2a/ln-handshake/0

```

### Additional Notes
* snapshot doesn't work at epoch boundry?
* failing on tool that produces writeset.
* writeset looks into db, and then fails.