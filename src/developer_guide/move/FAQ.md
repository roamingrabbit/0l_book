# FAQs

Using this as a basic scratch sheet for figuring out error messages.

## Errors and Fixes

**E**: It is still being borrowed
```
    ^ Invalid return. Resource 'State' is still being borrowed.
    ·
 81 │         let v = Vector::borrow(&st.hist, 0);
    │                 --------------------------- It is still being borrowed by this reference
```

**E**: * dereference
```
  public fun get(sender: &signer): u8 acquires State {
        let st = borrow_global<State>(Signer::address_of(sender));
        let elem = Vector::borrow(&st.hist, 0);
        // we need the * or else "It is still being borrowed by this reference"
        *elem
  }
```

---

**E**: How do you get transaction hashes / receipts
q txn_acc_seq 4C613C2F4B1E67CA8D98A542EE3F59F5 2 true
**F**: