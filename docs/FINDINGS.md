# Operation full gusto

Private Testnet-10 record. No seed, no private key, no wallet file.

The treasury is the Build receive address `[address]`. Every submit is checked against network `testnet-10` and `isSynced=true`. Outputs stay on receive indexes 0 through 21 of that same wallet.

## What the wallet did overnight

A desk mass sender had been spending this treasury. Confirmed balance samples:

| UTC | TKAS |
| --- | ---: |
| 2026-10-01 23:07:09 | 980,024.00 |
| 2026-10-01 23:38:36 | 899,710.11 |
| 2026-10-01 23:48:08 | 768,540.71 |
| 2026-10-01 23:57:38 | 583,109.11 |
| 2026-10-02 00:11:10 | 394,329.64 |
| 2026-10-02 00:19:48 | 143,518.09 |
| 2026-10-02 00:26:32 | 86,012.53 |
| 2026-10-02 00:33:11 | 550.08 |
| 2026-10-02 06:59:05 | 1.69909802 |

At 06:59 UTC the node still showed 12 confirmed UTXOs, all already spent by mempool transactions, plus about 3.47 TKAS sitting in three unconfirmed outputs. That was below the 100,000 TKAS reserve, so no new ramp was started.

## Launch reading

Funds were back on the address by 07:10 UTC on 2 Oct 2026. Five synced kaspad 2.1.0 nodes agreed.

| Node | Mempool | Normal feerate | Priority feerate | Confirmed TKAS | UTXOs |
| --- | ---: | ---: | ---: | ---: | ---: |
| muon-10 | 34,684 | 596 | 5,064 | 2,986,384.16 | 13,431 |
| vector-10 | 145,538 | 139 | 167 | 2,986,374.42 | 13,880 |
| proton-10 | 401,448 | 178 | 348 | 2,986,372.18 | 13,983 |
| neutrino-10 | 401,443 | 178 | 348 | 2,986,370.97 | 14,039 |
| boson-10 | 401,440 | 178 | 348 | 2,986,370.36 | 14,067 |

The coins were already cut into about 12,500 outputs near 200 TKAS. The largest was 241.69 TKAS. There was no single 300 TKAS coin left, so the prepare step has to combine pairs into 300 TKAS outputs.

The mass sender was stopped at 2026-10-02 07:05:43 UTC (`local_stop`) while it was still splitting at a logged storm rate of 18,557 sompi/gram. This run does not use that fee. It starts at the 100 sompi/gram relay floor and raises one step only when a submit is rejected for fee, or when a probe is accepted and still unconfirmed after 40 seconds while the node's normal quote is higher.

Submits go to the first synced testnet-10 node whose mempool is under 92,000. At this reading that is muon-10. Vector, proton, neutrino, and boson were already over that line. Sends pause at 85,000 and resume only under 70,000. Public kaspad 2.1.0 has panicked when a transaction is inserted into a mempool that is already past 100,000.

## Earlier ramp plan, now superseded

The first plan was a capped ramp: at most 800,000 TKAS, never under 100,000 TKAS left, about 2,000 outputs of 300 TKAS, then 10 / 25 / 50 / 100 / 200 tx/s. Prepare did reach 1,620 confirmed outputs of 300 TKAS at 100 sompi/gram (fee 3,781,400 sompi each) on synced kaspad 2.1.0. Those coins were then spent by other local senders on this same wallet.

| UTC | TKAS on the 21 receive indexes |
| --- | ---: |
| 2026-10-02 07:29:06 | 2,429,379.86 |
| 2026-10-02 07:59:32 | 1,309,251.44 |

About 1.12 million TKAS left the treasury in that half hour. One of those senders was quoting a priority feerate near 4,475,952 sompi/gram. The ramp's own prepare fees are a few TKAS, not that drop. A later 20,000 TKAS fee cap and the 100,000 TKAS reserve were both dropped.

## Empty-wallet order

The order after that plan is to push this Testnet-10 wallet until it is empty. No reserve. No 800,000 TKAS cap. One spender. Outputs stay on keys from the same wallet.

The live spender pauses new submits at mempool 85,000 and resumes only under 70,000. It does not submit to vector, proton, neutrino, or boson while those mempools are in the hundreds of thousands. The fee is `min(200,000, max(100, 2 × normal, priority))` sompi per gram, so it follows the priority quote without the multi-million spiral from earlier in the morning.

At 08:06 UTC a scan on muon-10 saw 476,421.31 TKAS. That process accepted 30,233 transactions, rejected 0, and paid 172,815.20 TKAS in fees before it paused at mempool 84,773 and was then stopped. Queued value at the pause was 149,515.11 TKAS.

A replacement mass sender started in its place and logged `sent=0` with more than 1,000 rejects on already-spent inputs. It was stopped. One drain was started again at 08:13 UTC.

Reading at 2026-10-02 08:15:24 UTC, synced kaspad 2.1.0 muon-10, mempool 77,615, disk free 638 GB:

| Field | Value |
| --- | ---: |
| Scan at start of this process | 184,312.62 TKAS |
| Queued still in hand | 68,171.11 TKAS |
| Accepted | 15,115 |
| Rejected | 0 |
| Rate | 138.2 tx/s |
| Fees this process | 86,301.09 TKAS |
| Feerate | 90,728 sompi/gram |

The run is still going. It stops when a rescan and a consolidate leave nothing to spend, or if the node leaves testnet-10, loses sync, or free disk falls under 10 GB.
