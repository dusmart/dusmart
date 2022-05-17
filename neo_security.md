# Risks found in NEO

almost all risks are reported with a POC [here](https://github.com/lazynode/Tanya/tree/main/PoC)

## neo

> These attacks were mainly discovered with vang1ong7ang and Hecate2. At first, vang1ong7ang guided us and we did the audits together. After the COVID-19 messed up Shanghai, I had to work from home and do auditing myself. They're sorted by revealing time.

type | location | reason | poc | issue | fix |  my contribution
---- | ---- | ------ | --- | ----- | --- | ----------
OOM | vm GC | faulty implementation of BFS | [poc](https://github.com/lazynode/Tanya/pull/1/files) | [issue](https://github.com/neo-project/neo-vm/issues/418) | [fix](https://github.com/neo-project/neo-vm/pull/416/files) | half
OOM | native contract stdlib's jsonSerialize | faulty implementation of checking size | [poc](https://github.com/lazynode/Tanya/pull/2/files) | [issue](https://github.com/neo-project/neo/issues/2527) | [fix](https://github.com/neo-project/neo/pull/2529/files) | few
DoS | vm GC | GC combined other slow operation O(n<sup>2</sup>) | [poc](https://github.com/lazynode/Tanya/pull/5) | [issue](https://github.com/neo-project/neo/issues/2532) | [fix](https://github.com/neo-project/neo-vm/pull/464/files) | main
Dos | vm GC | PickItem opcode in an end-to-end array's GC is O(n<sup>2</sup>) | [poc](https://github.com/lazynode/Tanya/pull/4/files) | [issue](https://github.com/neo-project/neo/issues/2528) | [fix](https://github.com/neo-project/neo-vm/pull/464/files) | few
OOM | native contract stdlib's deserialize | forget to limit object size | [poc](https://github.com/lazynode/Tanya/pull/6) | [issue](https://github.com/neo-project/neo/issues/2530) | [fix](https://github.com/neo-project/neo/pull/2531/files) | few
OOM | native contract stdlib's jsonDeserialize | forget to limit object size | [poc](https://github.com/lazynode/Tanya/pull/7/files) | [issue](https://github.com/neo-project/neo/issues/2533) | [fix](https://github.com/neo-project/neo/pull/2553) | few
OOM | vm clone opcode upon nested struct | huge object copy without limits | [poc](https://github.com/lazynode/Tanya/pull/8/files) | [issue](https://github.com/neo-project/neo-vm/issues/426) | [fix](https://github.com/neo-project/neo-vm/pull/423/files) | few
OOM | vm equal opcode upon nested struct | huge object test without limits | [poc](https://github.com/neo-project/neo-vm/issues/426#issuecomment-878120245) | [issue](https://github.com/neo-project/neo-vm/issues/426) | [fix](https://github.com/neo-project/neo-vm/pull/428/files) | main
Inappropriate GAS Price | vm sqrt opcode | inappropriate slow implementation | [poc](https://github.com/lazynode/Tanya/pull/9) | [issue](https://github.com/neo-project/neo-vm/issues/421) | [fix](https://github.com/neo-project/neo-vm/pull/427/files) | few
OOM | vm pow opcode | forget to limit exponent value | [poc](https://github.com/lazynode/Tanya/pull/10) | [issue](https://github.com/neo-project/neo-vm/issues/425) | [fix](https://github.com/neo-project/neo-vm/pull/422/files) | few
Potential Risk | NEP-17 standard | transfer hook makes attack easier | [poc](https://github.com/lazynode/Tanya/pull/12/files) | [issue](https://github.com/neo-project/neo-node/issues/822) | - | half
Information Leak | neo OracleService module | forget to check http redirect | [poc](https://github.com/lazynode/Tanya/pull/14/files) | [issue](https://github.com/neo-project/neo-modules/issues/693) | [fix](https://github.com/neo-project/neo-modules/pull/692/files) | few
OOM | neo json filter | do not realize filter result's explosion | [poc](https://github.com/lazynode/Tanya/pull/14/files)  | [issue](https://github.com/neo-project/neo/issues/2663) | [fix](https://github.com/neo-project/neo/pull/2665) | some
DoS | neo ApplicationLogs module | forget to limit result stack | [poc](https://github.com/lazynode/Tanya/pull/15/files) | [issue](https://github.com/neo-project/neo/issues/2666) | [fix](https://github.com/neo-project/neo-modules/pull/696) [fix](https://github.com/neo-project/neo/pull/2671/files) | main
Overflow | native contract ContractManagement update | update counter overflow | [poc](https://github.com/lazynode/Tanya/pull/16/files) | [issue](https://github.com/neo-project/neo/issues/2668) | [fix](https://github.com/neo-project/neo/pull/2697/files) | some
DoS | neo TokensTracker module | forget to limit GAS usage | [poc](https://github.com/lazynode/Tanya/pull/17) | [issue](https://github.com/neo-project/neo/issues/2670) | [fix](https://github.com/neo-project/neo-modules/pull/697/files) | main
DoS | neovm large struct equal opcode | forget to limit size | [poc](https://github.com/lazynode/Tanya/pull/19/files) | [issue](https://github.com/neo-project/neo/issues/2700) | [fix](https://github.com/neo-project/neo-vm/pull/454/files) | main
Manipulating Random | syscall random | random sequence is predictable | [poc](https://github.com/lazynode/Tanya/pull/22) | [issue](https://github.com/lazynode/Tanya/issues/24) | - | main
Manipulating Random | syscall random | side channel attack by GAS manipulating | [poc](https://github.com/neo-project/neo/issues/2693#issuecomment-1096021296) | [issue](https://github.com/neo-project/neo/issues/2693) | - | main
DoS | syscall CreateMultisigAccount | under-priced | [poc](https://github.com/neo-project/neo/issues/2710) | [issue](https://github.com/neo-project/neo/issues/2710) | [fix](https://github.com/neo-project/neo/pull/2712/files) | main
DoS | syscall CheckWitness | under-priced cache-miss | [poc](https://github.com/lazynode/Tanya/pull/27/files) | [issue](https://github.com/neo-project/neo/issues/2720) | TODO | main
DoS | opcodes in O(n) | under-priced | [poc](https://github.com/lazynode/Tanya/pull/28) | [issue](https://github.com/neo-project/neo/issues/2723) | TODO | main
**Money Print & Govenance Control** | native contract NeoToken | Reentrance | [poc](https://github.com/lazynode/Tanya/pull/31/files) | private submit | [fix](https://github.com/neo-project/neo/pull/2734) | main

* The **Reentrance** in NeoToken contract may print the NEO token in any amount. The same issue exists in the `Vote` method. We contact the core developer only at first and reveal it here after being fixed.
* The **Potential Risk** is by design. Therefore many APPs suffered from this. I've got a bug bounty from a big exchange and a bug bounty from dogerift thanks for it. The exchange refuse to make its name public. The **Reentrance** also benefits from this design.
* The random manipulation is discussed in [issue](https://github.com/neo-project/neo/issues/2693) with details. I post a POC to convice other developers for which I implemented a partial Murmur128 hash function on chain. My initial method can not attack those carefully-implemented dAPPs with RAUDefender. Roman-khimov's suggestion helped me to bypass the check.

# neo dAPPs

The following is the result I do audits on github or blockchain explorer.

## [gleeder](https://gleeder.app/)

* [GAS Consume](https://github.com/lazynode/Tanya/pull/21) with a few cost
* [DoS](https://github.com/lazynode/Tanya/pull/25) with no cost

After reporting with the developer, the first one has been considered at developing and can be expensive to avoid.

The second one is found after seeing the source code. Carefully checking is really needed in such contracts. Every bit in a transaction counts.

## [dogerift](https://dogerift.com/)

**Reentrancy attack**

When admin transfer his dogerift token to anyone, the token will try to call the recevier's `OnNep17Payment`. If the recevier is a contract and call back to the dogerift's contract. Then the check `Tx.Sender.Equals(owner)` will pass and successfully do anything as the attacker's wish.

Developer fixed it in [commit](https://github.com/DogeRift/DogeRift/commit/348eb09d73cf8c5add8847d3c8cad090add9bb85) and gived me a bug bounty.
