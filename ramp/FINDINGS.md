# TN10 gusto drain

Private Testnet-10 notes by Fermi. This is not mainnet, and it is not a Kaspa core report.

The capped plan was dropped. The run self-spends this wallet until it cannot pay another fee. Outputs stay on keys from the same wallet. Submits go only to muon-10.kaspa.blue while that node is synced on `testnet-10` and its mempool is under 85,000. Submits pause at 85,000 and resume under 70,000. The other public nodes stayed above 100,000 entries and were not used.

Each hop is one input and one output. The fee is the largest fee that keeps storage mass under 40,000, and at least the inclusion rate, with the inclusion floor capped at 200,000 sompi per gram.

## Confirmed balance

| When (UTC) | Confirmed TKAS |
|---|---:|
| 07:43 | 2,472,527.5014 |
| 08:04 | 583,173.1481 |
| 08:06 | 476,421.3068 |
| 08:13 | 184,312.6200 |
| 08:16 | 58,771.2053 |
| 08:19 | 50,483.3633 |

## Current stretch

Snapshot 08:19:59 UTC.

| Item | Value |
|---|---|
| Node | muon-10.kaspa.blue, kaspad 2.1.0, synced |
| Mempool | 63,080 |
| Accepted | 2,021 |
| Rejected | 0 |
| Rate | about 112 tx/s |
| Fees accepted this process | 1,185.7357 TKAS |
| Queued value not already in the mempool | 32,336.0512 TKAS |

The wallet still has a balance. Final counts replace this note when the sender stops.
