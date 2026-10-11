> **Experimental. We are just trying this.**
>
> Good intentions, shaky hands. STP does not know what he is doing. We test, we write down what we think we saw, and that is the whole product. A number here is not the truth. A chart is not the truth. Any other sentence that sounds sure of itself is not the truth either. Do not count any of it as a claim.
>
> [Disclaimer](DISCLAIMER.md)

# Full gusto, 2 Oct 2026

**Experimental. Not advice.** Testnet-10 only. This note has no keys, no addresses, and no transaction ids.

Full gusto is the spend ramp on the funded testnet-10 wallet. No local kaspad was listening. The client uses one synced public wRPC node whose mempool is under 92,000, and it pauses at 85,000.

## This morning, before the coins arrived

At 08:58 +02 the ramp was not started. Two synced kaspad 2.1.0 nodes agreed that receive index 0 held 1.69909802 tKAS in 12 UTXOs. Receive index 1 held 22.715214 tKAS. Indexes 2 through 30 were empty. Nothing was submitted. Fees were 0.

The same index 0 had shown 980,024.00330406 tKAS at 01:07 +02.

## After the coins arrived

Synced kaspad 2.1.0:

| Node | Virtual DAA | Mempool | Index 0 | UTXOs | Largest UTXO |
| --- | ---: | ---: | ---: | ---: | ---: |
| muon-10.kaspa.blue | 585928173 | 37083 | 2,548,420.40226822 tKAS | 11061 | 241.85582082 tKAS |
| vector-10.kaspa.green | 585928636 | 145636 | 2,838,365.92825357 tKAS | 12278 | 241.85582082 tKAS |

The gap is the two nodes not holding the same mempool. Vector, proton-10, neutrino-10, and boson-10 were all above 100,000. Public kaspad 2.1.0 has panicked on insert once a pool capped at 100,000 is already past that line. Those four nodes are not used for submits.

The desk mass sender had started spending the new coins. It was stopped so this ramp would not double-spend them. While it was stopped, muon fell from about 85,000 to 34,043 and the priority quote returned to 100 sompi per gram.

One 45 tKAS payment to receive index 1 was broadcast before the ramp, at 300 sompi per gram. Mass was 2036 and the fee was 610800 sompi. That coin is outside the ramp's working indexes.

## Ramp open

Boot at 2026-10-02T07:18:36Z. Network check passed on all five public nodes. The client kept muon-10, kaspad 2.1.0, synced, mempool 37778.

A second open at 07:19:20Z, after the first fanout had already moved coins into the mempool, read index 0 as 2,333,460.7274 tKAS across 144,538 UTXOs on the first count and then the later count. It selected 2,000 coins totaling 477,500.3901 tKAS and left the rest on index 0, above the 100,000 tKAS reserve. The 800,000 tKAS budget was not reached. Fee tier started at 100 sompi per gram. The first fanout batches were accepted with 0 rejects.

Working outputs are receive indexes 2 through 21. The steps are 10, 25, 50, 100, and 200 transactions per second, five minutes each, then the highest stable step for 60 minutes. Stable means at least 95 percent accepted and the node still synced. The run stops if the node loses sync, more than 10 percent are rejected for two minutes, free disk on C: drops under 10 GB, or the budget or reserve is hit.

The live CSV is on the desk as `stress-test-2026-10-02.csv`. This note will get the totals when the run reaches its final line.

## Open in progress, 07:44 UTC

Muon-10 was the only public node under the 92,000 mempool line. It reported kaspad 2.1.0, synced, mempool about 79,600. Vector-10 was about 145,000. Proton-10, neutrino-10, and boson-10 were about 393,000. Submits stay on muon-10.

1,833 coins totaling 463,558.8526 tKAS were already on receive indexes 2 through 21 from the earlier fan-out, which had accepted its batches at 100 sompi per gram with no rejects. This open uses those coins. It does not cut more from index 0. Index 0 still held about 2,005,246 tKAS, above the 100,000 reserve.

A second spender on the same wallet was submitting at the same time, with no reserve. Its transactions had already spent the coins this open tried to hop, so the first 10 tx/s submits were rejected as already in the mempool. That spender was stopped. Muon then crossed 85,000 and this open paused there, which is the planned pause. It stops if that pause lasts about two minutes.

The five rate steps and the 60-minute hold have not finished. Totals, fees, and the highest stable rate will be added when the final line is written.

## Max drain, 07:52 UTC

The reserve is off. This open spends receive indexes 0 through 21 until the wallet is empty. Submits stay on muon-10. The pause is 85,000 and the resume line is 70,000. The fee rate in use is 200,000 sompi per gram. A live priority quote was several million sompi per gram. These submits were still accepted at 200,000.

From 07:52:27Z to 07:52:44Z the open accepted 3,949 transactions and rejected 0. The rate peaked about 239 per second. Muon moved from about 67,000 to about 117,000, and the open paused. At 07:53:14Z muon was about 71,800 and the pause was still on. Queued value was about 570,150 tKAS. Fees counted about 661,719 tKAS. This open started from about 1,492,117 tKAS. It stops when the wallet is empty.

## Full wallet, 08:37 UTC

The 800,000 tKAS budget and the 100,000 tKAS reserve are off. One spender is running. It spends receive indexes 0 through 39 back onto those same keys. Submits stay on muon-10. The pause is 85,000 and the resume line is 70,000.

Indexes 22 through 39 still held 509,441.5 tKAS in 1,781 UTXOs, mostly pieces near 300 tKAS. A scan at 08:33:31Z covered indexes 0 through 39: 143,499 UTXOs and 539,204.92 tKAS. At 08:37:20Z the same process was paused with 538,192.36 tKAS still queued, 0 accepted and 0 rejected in that life. Muon-10 was kaspad 2.1.0, synced, mempool about 97,600, down from about 99,000. Vector-10 was about 210,000. Proton-10, neutrino-10, and boson-10 were about 450,000. Those four stay unused.

The fee quote at the pause was normal 363 and priority 3,109 sompi per gram. Free disk on the desk was 638 GB. Earlier the same drain, on indexes 0 through 21, accepted about 240 transactions per second with 0 rejects until muon filled. This open waits under 70,000, then spends until the queued coins cannot pay a fee.



---
Merged here on 11 Oct 2026 from `tn10-storm-2026-10-02-ledger` (formerly `tn10-gusto-ledger`, commit 1999e38), which is now archived: https://github.com/STP-KAS/tn10-storm-2026-10-02-ledger
