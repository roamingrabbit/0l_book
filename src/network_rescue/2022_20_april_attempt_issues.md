# 2022 20 April issues


## @nibbler 
validator error out (not running tower) 
log:
```
 20:     0x7f1b1a44b609 - start_thread
  21:     0x7f1b19e95163 - clone
  22:                0x0 - <unknown>
  
  
  2022-04-21T03:29:43.401096Z ERROR consensus/safety-rules/src/safety_rules.rs:491 {"error":"Unexpected error returned by secure storage: Internal error: Too many open files (os error 24)","event":"error","name":"construct_and_sign_vote","round":8892}
  2022-04-21T03:29:46.184395Z [consensus] ERROR common/crash-handler/src/lib.rs:38 details = '''panicked at 'Failed to persist commit: InternalError { error: "Service error: \"IO error: While open a file for appending: /home/0L/.0L/db/diemdb/2177609.log: Too many open files\"" }', consensus/src/block_storage/block_store.rs:223:14'''
  backtrace = '''
     0:     0x56443185213c - backtrace::capture::Backtrace::new::ha92e72667ec9fb7e
     1:     0x564431917fae - crash_handler::handle_panic::h6528425d40da96ce
     2:     0x564431917f2a - crash_handler::setup_panic_handler::{{closure}}::h2c9ce01f757d6013
     3:     0x564431d96c07 - std::panicking::rust_panic_with_hook::hb89f5f19036e6af8
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/std/src/panicking.rs:595:17
     4:     0x564431db2c73 - std::panicking::begin_panic_handler::{{closure}}::h119e7951427f41da
     5:     0x564431db2bec - std::sys_common::backtrace::__rust_end_short_backtrace::hce386c44bf47a128
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/std/src/sys_common/backtrace.rs:141:18
     6:     0x564431db2b9d - rust_begin_unwind
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/std/src/panicking.rs:493:5
     7:     0x56443190a080 - core::panicking::panic_fmt::h2242888e8769cd33
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/core/src/panicking.rs:92:14
     8:     0x56443190e112 - core::option::expect_none_failed::hb1edf11f73e63728
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/core/src/option.rs:1329:5
     9:     0x5644318df41a - <core::future::from_generator::GenFuture<T> as core::future::future::Future>::poll::hcd948f882d98a454
    10:     0x5644318dd6f5 - <core::future::from_generator::GenFuture<T> as core::future::future::Future>::poll::h5c263fe38f28ae47
    11:     0x5644318da569 - <core::future::from_generator::GenFuture<T> as core::future::future::Future>::poll::h8baceb1bed30e07f
    12:     0x5644318cd923 - <core::future::from_generator::GenFuture<T> as core::future::future::Future>::poll::hb40d7b223e7b4560
    13:     0x5644318efd26 - tokio::runtime::task::harness::poll_future::hfb4fc55b62dad31f
    14:     0x5644318ee8ea - tokio::runtime::task::raw::poll::hb5f3b1a410c1be4b
    15:     0x564431dd5b58 - tokio::runtime::thread_pool::worker::Context::run_task::h9108183345588446
    16:     0x564431de02c2 - tokio::runtime::task::raw::poll::h0c81b8769eb62609
    17:     0x564431dda2ea - std::sys_common::backtrace::__rust_begin_short_backtrace::h20be9e383db8b6fe
    18:     0x564431ddb993 - core::ops::function::FnOnce::call_once{{vtable.shim}}::h91085810c12e01b2
    19:     0x564431dc0a35 - <alloc::boxed::Box<F,A> as core::ops::function::FnOnce<Args>>::call_once::hc444a77f8dd8d825
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/alloc/src/boxed.rs:1546:9
                             <alloc::boxed::Box<F,A> as core::ops::function::FnOnce<Args>>::call_once::h8b68a0a9a2093dfc
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/alloc/src/boxed.rs:1546:9
                             std::sys::unix::thread::Thread::new::thread_start::hb95464447f61f48d
                                 at /rustc/9bc8c42bb2f19e745a63f3445f1ac248fb015e53/library/std/src/sys/unix/thread.rs:71:17
    20:     0x7f1b1a44b609 - start_thread
    21:     0x7f1b19e95163 - clone
    22:                0x0 - <unknown>
  '''
  
  
  ---
restarted validator 2022-04-21 12:30 EST
```
```
====================================== 9843 ======================================
[move print] 100100
[move print] 200100
[move print] 200110
[move print] 200120
[move print] 200130
[move print] 200131
[move print] 200132
[move print] 200133
[move print] 200134
[move print] 200140
[move print] 200150
[move print] 300100
[move print] 400100
[move print] 500100
[move print] 500110
[move print] 600100
[move print] 700100
[move print] 900200
2022-04-21T16:23:55.961830Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 7ec16859 at /ip4/35.231.138.89/tcp/6180/ln-noise-ik/987f636ef651abc3bc0ad1a33ef2e5841768fde064971333059d84442bb3d576/ln-handshake/0: Transport error: timeout elapsed {"error":"Transport error: timeout elapsed","network_address":"/ip4/35.231.138.89/tcp/6180/ln-noise-ik/987f636ef651abc3bc0ad1a33ef2e5841768fde064971333059d84442bb3d576/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"7EC16859C24200D8E074809D252AC740"}
2022-04-21T16:24:00.929110Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 46a7a744 at /ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0: Transport error: timeout elapsed {"error":"Transport error: timeout elapsed","network_address":"/ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"46A7A744B5D33C47F6B20766F8088B10"}
2022-04-21T16:24:46.227506Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 7ec16859 at /ip4/35.231.138.89/tcp/6180/ln-noise-ik/987f636ef651abc3bc0ad1a33ef2e5841768fde064971333059d84442bb3d576/ln-handshake/0: Transport error: timeout elapsed {"error":"Transport error: timeout elapsed","network_address":"/ip4/35.231.138.89/tcp/6180/ln-noise-ik/987f636ef651abc3bc0ad1a33ef2e5841768fde064971333059d84442bb3d576/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"7EC16859C24200D8E074809D252AC740"}
2022-04-21T16:24:46.232082Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 46a7a744 at /ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0: Transport error: timeout elapsed {"error":"Transport error: timeout elapsed","network_address":"/ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"46A7A744B5D33C47F6B20766F8088B10"}
```

Keep erroring out and need to restart validator
`RUST_LOG=error diem-node -f ~/.0L/validator.node.yaml >> ~/.0L/logs/validator.log 2>&1`

```
====================================== 9843 ======================================
[move print] 100100
[move print] 200100
[move print] 200110
[move print] 200120
[move print] 200130
[move print] 200131
[move print] 200132
[move print] 200133
[move print] 200134
[move print] 200140
[move print] 200150
[move print] 300100
[move print] 400100
[move print] 500100
[move print] 500110
[move print] 600100
[move print] 700100
[move print] 900200
2022-04-21T18:17:08.081901Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 7ec16859 at /ip4/35.231.138.89/tcp/6180/ln-noise-ik/987f636ef651abc3bc0ad1a33ef2e5841768fde064971333059d84442bb3d576/ln-handshake/0: Transport error: timeout elapsed {"error":"Transport error: timeout elapsed","network_address":"/ip4/35.231.138.89/tcp/6180/ln-noise-ik/987f636ef651abc3bc0ad1a33ef2e5841768fde064971333059d84442bb3d576/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"7EC16859C24200D8E074809D252AC740"}
2022-04-21T18:17:12.781234Z [network-Validator] ERROR network/src/peer_manager/mod.rs:1227 [validator,Validator,34b5d5e5] Outbound connection failed for peer 46a7a744 at /ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0: Transport error: timeout elapsed {"error":"Transport error: timeout elapsed","network_address":"/ip4/35.192.123.205/tcp/6180/ln-noise-ik/da9ea456e1d9f45810669ecfcdb9f75a4d828a7e7a97f68014f47d789972a710/ln-handshake/0","network_context":{"role":"validator","network_id":"Validator","peer_id":"34b5d5e56ec27d954ac5d40b24d11422"},"remote_peer":"46A7A744B5D33C47F6B20766F8088B10"}
```
### @nibber Fix
thanks to @drawks & @OD
was a RAM issue had 4GB and on network sync it would crash
```
free -h
              total        used        free      shared  buff/cache   available
Mem:          3.8Gi       3.5Gi       104Mi       0.0Ki       185Mi        85Mi
Swap:            0B          0B          0B
```
upgraded box to 8GB (2 cores) running sync brought it down free mem to 897Mi
```
free -h
              total        used        free      shared  buff/cache   available
Mem:          7.8Gi       6.7Gi       127Mi       0.0Ki       923Mi       897Mi
Swap:            0B          0B          0B
```
Successful Start log from 2022 20 April


```
2022-04-20T21:25:10.678234Z [state-sync] ERROR state-sync/src/coordinator.rs:1314 {"error":"SyncedBeyondTarget(37235488, 37235488)","name":"send_chunk_request"}
====================================== 2 ======================================
[move print] 100100
[move print] 200100
[move print] 200110
[move print] 200120
[move print] 200130
[move print] 200131
[move print] 200132
[move print] 200133
[move print] 200134
[move print] 200140
[move print] 200150
[move print] 300100
[move print] 400100
[move print] 500100
[move print] 500110
[move print] 600100
[move print] 700100
[move print] 900200
0L ==== stdlib upgrade: checking for stdlib upgrade
====================================== 3 ======================================
[move print] 100100
```

### @thenateway
i changed one thing in my config
that i had never really understood what it did
i had this hardcoded waypoint info (which always seemed to work before these mainnet issues):

```
waypoint:
  from_config: "8567508:fdb9f2b120e7527dd6c8725533ab686500a8ccbeaf111088ebe2f46c18b3f4f2"
```
and then i switched it to:

```
waypoint:
  from_storage:
    type: on_disk_storage
    path: /home/node/.0L/key_store.json
    namespace: e264023342b41accdbb61a190b6cb2a7-oper
```