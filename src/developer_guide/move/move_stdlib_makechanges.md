# Move stdlib
[TODO] - Not really stdlib, base framework? Or do we call them Move stdlib, OL stdlib, Diem stdlib?

The move stdlib modules for the 0L network lives under the [language/diem-framework/modules](https://github.com/OLSF/libra/tree/main/language/diem-framework/modules) 
directory. The modules include the base modules for the original diem network as well as the 0L additions: [0L](https://github.com/OLSF/libra/tree/main/language/diem-framework/modules/0L) 
and [0L transaction scripts](https://github.com/OLSF/libra/tree/main/language/diem-framework/modules/0L_transaction_scripts) 

The stdlib consists of `modules` and `scripts`. See the documentation of the current `modules` and `scripts`
[here](https://github.com/OLSF/libra/tree/main/language/diem-framework/releases/artifacts/current/docs)

## Build The stdlib
```console
$ cd libra/language/diem-framework
$ cargo build
$ cargo run

NOTE: run this program in --release mode for better speed
Extracting linking/layout APIs from old module bytecodes ... (took 0.000s)
Compiling modules ... (took 15.771s)
Checking linking/layout compatibility ... (took 0.000s)
Generating module docs ... (took 23.920s)
Generating script docs ... (took 22.263s)
Generating script ABIs ... (took 22.149s)
Generating Rust script builder ... (took 0.414s)
Generating error explanations ... (took 20.986s)
```

or 

```console

$ cd libra/target/debug
$ ./diem-framework 

NOTE: run this program in --release mode for better speed
Extracting linking/layout APIs from old module bytecodes ... (took 0.045s)
Compiling modules ... (took 18.148s)
Checking linking/layout compatibility ... (took 0.008s)
Generating module docs ... (took 22.826s)
Generating script docs ... (took 20.267s)
Generating script ABIs ... (took 20.335s)
Generating Rust script builder ... (took 0.438s)
Generating error explanations ... (took 21.328s)
```

## View The stdlib 
```console
$ cd libra/language/diem-framework/releases/artifacts/current/modules

$ ls

000_Signer.mv                          011_Event.mv                           022_StagingNet.mv                      
033_XDX.mv                             044_Authenticator.mv                   055_Bonding.mv                        
 066_DiemBlock.mv                       077_SystemAdministrationScripts.mv
001_Errors.mv                          012_DiemConfig.mv                      023_Hash.mv                            
034_TransactionFee.mv                  045_SharedEd25519PublicKey.mv          056_BridgeEscrow.mv                    
067_DiemConsensusConfig.mv             078_TestFixtures.mv
002_CoreAddresses.mv                   013_RegisteredCurrencies.mv            024_GAS.mv                            
 035_Receipts.mv                        046_RecoveryAddress.mv                 057_BridgeScripts.mv                   
 068_DiemVMConfig.mv                    079_TowerStateScripts.mv
003_DiemTimestamp.mv                   014_Diem.mv                            025_Globals.mv                         
036_FIFO.mv                            047_AccountAdministrationScripts.mv    058_Burn.mv                            
069_DiemVersion.mv                     080_TransferScripts.mv
004_SlidingNonce.mv                    015_AccountLimits.mv                   026_TowerState.mv                      
037_DualAttestation.mv                 048_AccountCreationScripts.mv          059_DemoScripts.mv                     
070_Upgrade.mv                         081_TreasuryComplianceScripts.mv
005_Signature.mv                       016_XUS.mv                             027_ValidatorUniverse.mv               
038_DiemTransactionPublishingOption.mv 049_AccountScripts.mv                  060_Migrations.mv                      
071_Oracle.mv                          082_ValidatorAdministrationScripts.mv
006_Roles.mv                           017_Option.mv                          028_NodeWeight.mv                      
039_DiemId.mv                          050_AutoPay.mv                         061_MigrateTowerCounter.mv             
072_Genesis.mv                         083_ValidatorScripts.mv
007_FixedPoint32.mv                    018_ValidatorOperatorConfig.mv         029_Cases.mv                           
040_DesignatedDealer.mv                051_Audit.mv                           062_Subsidy.mv                        
 073_Mock.mv                            084_WalletScripts.mv
008_Vector.mv                          019_ValidatorConfig.mv                 030_DiemSystem.mv                      
041_ChainId.mv                         052_AutoPayScripts.mv                  063_FullnodeSubsidy.mv                 
074_OracleScripts.mv
009_Testnet.mv                         020_VDF.mv                             031_Wallet.mv                         
 042_AccountFreezing.mv                 053_Decimal.mv                         064_Epoch.mv                          
  075_PaymentScripts.mv
010_BCS.mv                             021_Stats.mv                           032_VASP.mv                            
043_DiemAccount.mv                     054_Debug.mv                           065_EpochBoundary.mv                   076_PersistenceDemo.mv

```

## View Scripts
```console
$ cd libra/language/diem-framework/releases/artifacts/current/script_abis

$ ls 

AccountAdministrationScripts   PaymentScripts                 TreasuryComplianceScripts      ol_account                     
ol_bridge                      ol_miner_state                 ol_transfer                    ol_wallet
AccountCreationScripts         SystemAdministrationScripts    ValidatorAdministrationScripts ol_autopay                     
ol_demo_e2e                    ol_oracle                      ol_validator
```