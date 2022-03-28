# move

Smart contract language with formal verification and the idea of ownership baked into its programming model.

The stdlib for the 0L network is written in move. The stdlib defines some of the core protocol of the network, and 
is able to be upgrade on the running network with a 2/3rd validator vote. The `stdlib` defines basic protocol rules:
consensus, account creation, tx validation, etc. [see move_stdlib.md](move_stdlib.md)

## Modules and Resources

### Modules
[The Move Book - modules](https://move-book.com/syntax-basics/module.html)
deployed to an address, e.g. `0x1{}` there is one copy of these and they can be referenced from scripts, or resources.
new types and resources can only be defined inside modules.
accessible to for others.
```Move
address 0x1 {
  module Math {
      // module contents
  
      public fun sum(a: u64, b: u64): u64 {
          a + b
      }
  }
}
```

import
direct
`0x1::<Module_Name>::<Resource|Type>`
or
```
use <Address>::<ModuleName>;

# access
ModuleName::{Method | Type};
```

### Resources
[see move book resource](https://move-book.com/resources/what-is-resource.html?highlight=resource#what-is-resource)

> type with set of restrictions created to make this type safe enough to represent digital assets.

non-copyable and non-droppable
and
storable and transferable between accounts

```rust
module M {
    struct T has key, store {
        field: u8
    }
}
```
## Move Traits
[see move-book types with abilities](https://move-book.com/advanced-topics/types-with-abilities.html)

**Copy** - value can be copied (or cloned by value).  
**Drop** - value can be dropped by the end of scope.  
**Key** - value can be used as a key for global storage operations.  
**Store** - value can be stored inside global storage.  

## Move Resources

[Mysten labs awesome move](https://github.com/MystenLabs/awesome-move)

[The move book](https://move-book.com/introduction/foreword.html)