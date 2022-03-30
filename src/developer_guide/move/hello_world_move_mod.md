# "Hello, World!" move module

Our "Hello, world!" Move module will be a simple key value store. A move module that can set a value and retrieve a value.
We will use it to store things we are grateful for on chain.

## Persistence "Hello, World!" Move module.
See [writing_and_publishing_thirdparty_module](https://github.com/OLSF/libra/blob/main/ol/documentation/move-dev/writing_and_publishing_thirdparty_modules.md)  
uses `key` trait <a href="index.html#move-traits">see</a>
```Rust
//! account: alice, 1000000, 0, validator
//! account: bob, 1000000, 0, validator

// module {{default}}::PersistenceDemo{

// address will change based on the address you are deploying to, if running the 
// testnet, you'll see the address printed out when the testnet starts up.

module 0x4C613C2F4B1E67CA8D98A542EE3F59F5::PersistenceDemo {
        use 0x1::Vector;
        use 0x1::Signer;
       // use 0x1::Testnet::is_testnet;
    
        // In Move the types for data storage are `resource struct`. Here a type 
        // State is being defined. Once a type is initialized in the global state, 
        // the resource is treated as if in-memory on the heap, the libra database 
        // is abstracted. The data is namespaced by an "access path" which includes 
        // the module name and user address. No special APIs are necessary for 
        // reading from the database, except permissioning each function which 
        // accesses a given struct, more below.
        struct State has key {
          hist: vector<u8>,
        }

        // The operation can only be performed on testnet
        // const ETESTNET : u64 = 04001;

        // For this demo, the `initialize` function writes a PersistenceDemo::State 
        // resource at the "sender" address. The access path will be 
        // <sender address>/PersistenceDemo/State/
        public fun initialize(sender: &signer){
          // `assert can be used to evaluate a bool and exit the program with an 
          // error code, 
          // e.g. testing if this is being run in testnet, and throwing error 01.
          // assert(is_testnet(), Errors::invalid_state(ETESTNET));
          // In the actual module, must assert that this is the sender is the 
          // association
          move_to<State>(sender, State{ hist: Vector::empty() });
        }


        // To read or write to a Resource Struct an `acquires` tag is 
        // needed to permission a function. 
        // NOTE all downsteam functions will also need permission on that 
        // data struct, i.e. need the same `acquires` parameters.
        public fun add_stuff(sender: &signer ) acquires State {
          //assert(is_testnet(), Errors::invalid_state(ETESTNET));

          // Resource Struct state is always "borrowed" and "moved" and 
          // generally cannot be copied. 
          // A struct can be mutably borrowed, if it is written to, 
          // using `borrow_global_mut`. 
          // Note the Type State
          let st = borrow_global_mut<State>(Signer::address_of(sender));
          // the `&` as in Rust makes the assignment to a borrowed value. Each Vector 
          // operation below with use a st.hist and return it before the 
          // next one can execute.
          let s = &mut st.hist;

          // Move has very limited data types. Vector is the most sophisticated and 
          // resembles a simplified Rust vector.  Can be thought of as an array 
          // of a single type.
          Vector::push_back(s, 1);
          Vector::push_back(s, 2);
          Vector::push_back(s, 3);
        }

        // Similar to above, except removing state.
        public fun remove_stuff(sender: &signer) acquires State{
          //assert(is_testnet(), Errors::invalid_state(ETESTNET));
          let st = borrow_global_mut<State>(Signer::address_of(sender));
          let s = &mut st.hist;

          Vector::pop_back<u8>(s);
          Vector::pop_back<u8>(s);
          Vector::remove<u8>(s, 0);
        }

        // Here are examples of read operations. Note the `aquires` here again.
        public fun isEmpty(sender: &signer): bool acquires State {
          //assert(is_testnet(), Errors::invalid_state(ETESTNET));

          // Note this is not a mutable borrow. Read only.
          let st = borrow_global<State>(Signer::address_of(sender));
          Vector::is_empty(&st.hist)
        }

        // Showing the Vector::length method
        public fun length(sender: &signer): u64 acquires State{
         // assert(is_testnet(), Errors::invalid_state(ETESTNET));
          let st = borrow_global<State>(Signer::address_of(sender));
          Vector::length(&st.hist)
        }

        // Showing the Vector::contains method
        public fun contains(sender: &signer, num: u8): bool acquires State {
          //assert(is_testnet(), Errors::invalid_state(ETESTNET));
          let st = borrow_global<State>(Signer::address_of(sender));
          Vector::contains(&st.hist, &num)
        }

    }
```

### Transaction Scripts 
Interacting with deployed Move modules.

Now that the Move module has been deployed we can interact with it via Move *Transaction Scripts*.

**note:** replace `{{default}}` with your address, e.g. `0x4C613C2F4B1E67CA8D98A542EE3F59F5`
Demo1 `add_stuff` assert that 3 items were added, 1,2,3.
```Rust
//! new-transaction
//! sender: alice
script {
    use {{default}}::PersistenceDemo;
    
    // This sender argument was populated by the test harness with a random address 
    // for `alice`, which can be accessed with sender variable or the helper `{alice}`
    fun main(sender: signer){ // alice's signer type added in tx.
      let sender = &sender;
      PersistenceDemo::initialize(sender);
      PersistenceDemo::add_stuff(sender);
      assert(PersistenceDemo::length(sender) == 3, 0);
      assert(PersistenceDemo::contains(sender, 1), 1);
    }
}
```
Demo2 check that there are not 2 items in the state. 
TODO: check VM error codes.
```Rust
///// The tags with `check` matches to a string in the VM output. Here we are checking 
// for a correct execution.
// check: EXECUTED

//! new-transaction
//! sender: alice
script {
    use {{default}}::PersistenceDemo;
    fun main(sender: signer){
        let sender = &sender;
      assert(PersistenceDemo::length(sender) == 2, 4);
    }
}

///// Checking the VM output for the string ABORTED

// check: ABORTED
```

Demo 3 fails because not initialized
```Rust
///// DEMO 3: State is not initialized in BOB address
///// this will fail because bob does not have the data struct, and we tried to 
//// operate on it.  This is a new transaction.

//! new-transaction
//! sender: bob
script {
    use {{default}}::PersistenceDemo;
    fun main(sender: signer){
        let sender = &sender;
        PersistenceDemo::add_stuff(sender);
    }
}

///// Checking the VM output for the string `EXECUTION_FAILURE`

// check: EXECUTION_FAILURE
```

