# Interacting With Move Module

In the previous section, we deployed a move module to our running testnet. Transaction scripts are the 
way that users interact with Move Modules.

| Variable | Value for the Example          |
|--|--------------------------------|
| Address | `0x4C613C2F4B1E67CA8D98A542EE3F59F5` |
| Tranasction Script Ref Page |    <a href="hello_world_move_mod.html">See Hello, World move module</a>                             |

### Transaction Scripts 

#### Compile Script
**note**: when compiling a script, make sure to include the dependent modules, if you deployed a module, make sure 
it is included in the dependencies with the same address. `module 0x4C613C2F4B1E67CA8D98A542EE3F59F5::PersistenceDemo`
```console
$ diem% dev compile <FULL_PATH>/Demo1.move <FULL_PATH_TO_LIBRA_PROJ>/libra/language/move-stdlib/modules
$ diem% dev compile  /Users/libby/Workspace.Libra/libra/Libby/movemods/Demo1.move /Users/libby/Workspace.Libra/libra/language/move-stdlib/modules /Users/libby/Workspace.Libra/libra/Libby/movemods/PersistenceDemo.move

    Finished dev [unoptimized + debuginfo] target(s) in 1.03s
     Running `target/debug/move-build /Users/libby/Workspace.Libra/libra/Libby/movemods/Demo1.move -o /var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/a7757976900af221d8c7754bbbacdb08 -d /Users/libby/Workspace.Libra/libra/language/move-stdlib/modules -d /Users/libby/Workspace.Libra/libra/Libby/movemods/PersistenceDemo.move`
Successfully compiled a program at:
  /var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/a7757976900af221d8c7754bbbacdb08/scripts/main.mv
  
```

### Execute Compiled Move Script
```console
$ diem% dev execute 4C613C2F4B1E67CA8D98A542EE3F59F5  /var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/a7757976900af221d8c7754bbbacdb08/scripts/main.mv
.......................................................................................................................................................................................................................................
Successfully finished execution

// 2nd time
diem% dev execute 4C613C2F4B1E67CA8D98A542EE3F59F5  /var/folders/mx/6jxkfzlx4rbdlqg4lhwj74mm0000gn/T/a7757976900af221d8c7754bbbacdb08/scripts/main.mv
..............................................................................................................................................................................................................................................
Transaction failed to execute; status: ExecutionFailure { location: "4C613C2F4B1E67CA8D98A542EE3F59F5::PersistenceDemo", function_index: 2, code_offset: 3 }!
```


### Querying 
```console
diem% q account_state 0x4C613C2F4B1E67CA8D98A542EE3F59F5
```