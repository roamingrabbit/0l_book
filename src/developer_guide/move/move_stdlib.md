# 0L move stdlib

The 0L move stdlib is deployed to the `0x1` address of the 0L network. 

The stdlib includes a block prologue that is executed at the start of every block.

## Changes Made By 0L Network

Upgrades voted on

Removed root acct

Move: add decimal rust lib

Move: +chia VDF verifier to VM (verify delay towers)

Autopay - payments in future

+restore - snapshot fullnode sync from epic

Carpe - wallet + light miner

## Move stdlib modules

`Signer.move`: wrapper around address

`BCS.move`: utility for converting a MOVE val into its binary rep in BCS (Binary Canonical Serialization) see common/bcs

`Event.move`

`FixedPoint32.move`: 32 bit integer part, 32 bit fractional bits.

`Vector.move`

`Option.move`:

`Error.move`: 0l added ol_tx and ol errors.

`Hash.move` // natively declared in move runtime.


## 0L stdlib Code
[Diem modules diem-framework/modules/](https://github.com/OLSF/libra/tree/main/language/diem-framework/modules)   
[0L diem-framework/modules/0L](https://github.com/OLSF/libra/tree/main/language/diem-framework/modules/0L)   
[0L diem-framework/0L transaction scripts](https://github.com/OLSF/libra/tree/main/language/diem-framework/modules/0L_transaction_scripts)
