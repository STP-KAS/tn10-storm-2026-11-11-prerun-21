> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · Kaspa Testnet-10 only; tKAS has no value.
>
> **This is the playbook for pre-run 21.** It is not Wednesday. It is not Tuesday. It is not pre-run 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, or 20. It does not start a machine and it does not arm one.

# Playbook

Who does what, and the gates before each machine may start. The plan is [plan/PLAN.md](plan/PLAN.md), the locks are [locks/LOCKED.md](locks/LOCKED.md), and the go files are the three GO pages. This page does not override them.

## Oversight

TN10 ops oversees this rehearsal end to end: Mini, the desk (Build), and the bot. TN10 only. Never mainnet. Do not edit the Tuesday repo, the Wednesday repo, or pre-run 1's to 20's go files. Do not write `REVIEW_CLOSED`.

For pre-run 21 the operator does not paste. On 2026-11-12 he asked TN10 ops for covenant pre-runs under congestion and competition, pre-run 11 and then 12, 13 or more as needed (voice, 09:06 and 09:09 Brussels time), and at 10:04 in chat said "Keep exploring". That is the arm. The agents start their runners once the gates are facts.

## Start gates

1. **Mini node synced.** Existing TN10 kaspad, existing data, no wipe. `isSynced` true, DAA moving.
2. **Desk node synced.** Existing private TN10 kaspad, existing data, loopback only, started with `pwsh`. No wipe. Synced, DAA moving.
3. **No other runner.** No earlier runner, waiter, or counter on any machine. Lane above the abort line. The desk's private candidate list is present and not empty (`HELD candidates-missing` otherwise).
4. **Hashes.** `hashes/SIXTEEN.md` with sixteen rows and an On origin line, from [tools/sixteen](tools/sixteen/README.md).
5. **Open.** The desk pushes `logs/PRE-RUN-OPEN.md`. Mini then pushes `logs/MINI-ARMED.md`.
6. **Counter, families, senders.** The desk runner starts the counter on its private node and waits for its start line (`HELD counter-down` otherwise). Then the genesis from the bundle that wrote `hashes/SIXTEEN.md`, the families, and the payment steps.

## Who does what

| Who | Role | What not to do |
|---|---|---|
| **Desk (Build)** | Sends the sixteen families (four fixed tiers, one path, one build, kit24) and runs our own heavy lane in one lane process (one lane; the operator's OK, calibrated first). No payments. Its private TN10 node counts what the chain accepted (lock line (iv)) and its probe reads the mempool (xii). Publishes `hashes/SIXTEEN.md`, `logs/PRE-RUN-OPEN.md`, `counts/desk/` per step, `counts/chain/TIMELINE.md` and `MEMPOOL.md` after the tail, and `logs/METHOD.md`. | Do not stop or wipe the desk node. No Windows PowerShell 5.1, no `KaspaPublicNode`, no miner, no devnet. No 8- or 32-family publisher. No second runner. Never restart the runner mid-run. No payment sender. No heavy lane other than the runner's own lane process (which carries both lanes). |
| **Mini** | Second chain read on its own node. Does not send, mine, or hold a key. Publishes `logs/MINI-ARMED.md`, then `counts/mini/` when the matching desk file is on origin. | Do not wipe. Do not repeat the desk's head as Mini's. |
| **Bot (TN10 ops)** | Sends payments in the HOLD-4 minute only, on a synced public kaspad that is not one the desk kept, or publishes a legal `NO SEND`. | Do not send in any other step. One waiter. No local node. |

## Status when this repo was opened

Not a gate. Read on 2026-11-13 between 08:58Z and 09:12Z. This is our own TN10 testing; status lines are what we read on our own machines.

- Mini: existing TN10 kaspad 2.1.0 up, no wipe. Pre-run 20's Mini runner ended on its own after its tail (08:52:40Z); pre-run 21's Mini runner starts only after that was read again.
- Desk: existing private TN10 kaspad 2.1.0 up with `pwsh`, no wipe. It is not stopped for this pre-run. Pre-run 20's runner ended on its own at 08:43:06Z. `serve.mjs` and its keeper are not touched.
- Box: no local TN10 node. No bot waiter running.
- **Housekeeping before this repo (the operator's OK, 2026-11-13 08:06 Brussels: "do what is best needed", and 09:49: keep going).** All between our own keys, none rejected, rate 100, recorded privately on the desk:
  - Key 0's coins of 10 tKAS or less (2,030 of up to 3 tKAS, 4,922 tKAS; 1,796 of 3–10, 11,317 tKAS) were merged into coins of about 20 tKAS (58 transactions, 4.61 tKAS in fees), 09:02Z.
  - **The sink is swept again.** Pre-run 20's 11,476 sink outputs (**430.35 tKAS**) went back to the payment key (key 16): 137 transactions of 84 inputs, **12.90 tKAS** in fees. Key 16's small coins (540, 1,168 tKAS) were then merged into coins of about 20 (9 transactions, 0.63 tKAS).
  - Keys 1–15 got a fresh genesis coin from key 0 (15 transactions, none rejected), 09:04:30Z.
  - Key 0's 1,610 coins of 10–16 tKAS were merged in pairs (805 transactions, 2.21 tKAS in fees), 09:04:55Z, because the runner counts each coin over 3 tKAS less 3 tKAS: fewer, larger coins leave more usable tKAS for the families.
- **Family lane** (key 0), after the merges: 2,275 coins (all 16–40 tKAS), **43,205 usable**. **Refilled from the payment pile** 09:10:37Z (`refill21.mjs`): 19 transactions, none rejected, 370 pile coins (7,530 tKAS) to key 0 at the same sizes, 0.85 tKAS in fees. After: key 0 2,645 coins over 3 tKAS, **49,612 usable**, no small coins; payment pile **695 coins, 13,814 tKAS**.
- **Budget.** The families use about 760 usable tKAS a family minute, and the runner asks for 8,000 over the 18,000 line at the end. This run plans **30 family minutes**. Read-only check `budget21.mjs`, 09:11Z: 49,612 − 760 × 30 = **26,812 projected at the end**, over 26,000: ok. The runner repeats this check before genesis and holds the run if it fails.
- **Why the cap test uses 8 chains, not 30.** With 30 chains the lane lands about 510–550 a minute; at 2,000 that is about 2,750 tKAS a minute, and the cap guard needs at least four minutes there, on top of about 760 a minute for the families. We do not hold that. With 8 chains the lane lands about 225–245 a minute whatever its rate (pre-run 20), about 1,230 tKAS a minute at 2,000. The guard and the freeze are the same code either way.
- **The lane's budget.** Fee cap **9,500 tKAS**, moved cap 10,000, pile floor 1,000 (pre-run 20: 12,000 / 13,000 / 3,000). Two decisions after the cap guard's reset, the runner lowers the lane's fee cap on purpose (to its fees so far plus 20 tKAS), so that the lane stops at a cap and `FROZEN` is exercised live.
- **Hop calibration on the node** (kit24, unchanged since pre-run 17), 09:11:00Z: one calibration covenant on key 0 (launch path `…-p21-cal`, not one of the sixteen families and not in `SIXTEEN.md`), its genesis, then two hops built by the family path and submitted on the desk's private node, each read back from the desk mempool:

| Hop | Builder bill rate (on 13,046) | kit24 storage mass | Node storage mass | Node compute mass | Fee, sompi | Node rate (fee ÷ node mass) |
|---|---:|---:|---:|---:|---:|---:|
| family 1 at 100 | 319 | 41,573 | 41,573 | 9,123 | 4,161,674 | 100.11 |
| family 13 (r450) at 450 | 1,434 | 41,564 | 41,564 | 9,123 | 18,707,964 | 450.10 |

  Storage mass matched to the unit and both node rates were within 1 percent of the asked rate (and not under it).
- **Our heavy lane's calibration:** at 2,000, 09:11:06Z: SDK storage mass 266,777, node 266,777 (0.00 percent off), compute 2,036, node rate 2,000.00 (fee 5.34 tKAS). At 100, 09:11:12Z: 266,672 on both sides, node rate 100.00. The sink key is the same one (swept before this run).
- The re-read just before `PRE-RUN-OPEN` (nodes synced, the Mini runner gone, the bot's free check) is recorded in the offline rehearsal section below.
- Known risks, not fixed mid-run:
  - Our lane slows other TN10 users' transactions at fees up to about its own rate while it runs. This run takes it to 2,000 on purpose for about five minutes. The operator OK'd our lane; the lane's fees are capped at 9,500 tKAS, the cap guard puts it back to 150 after 4 decided minutes at the cap, and the lane stops before the drain.
  - Short segments: BASE 2 minutes, a 2-minute reference (one decided minute), 2 + 2 minutes for the template probe, 10 for the cap test. One run.
  - The cap test steps × 2 from 600 (not × 1.25 from 150) to reach the cap within the budget; that is a choice of ours, not how the earlier runs climbed.
  - A submit cap paces our lane evenly, so with 15 or 30 chains fewer of them may be waiting at once than the chain count suggests; the probe and the template watcher read how many of ours are actually in the mempool.
  - The outside heavy fee-100 stream may also be there.
  - The rule reacts to the minute just closed and takes effect about 22 seconds into the next one.
  - The probe and the template watcher read the desk node's mempool and template, not a miner's.
  - Only two unique public kaspads answered in every check so far, and the desk keeps both, so the bot is expected to file `NO SEND no-free-node`.

## Offline rehearsal, recorded before `PRE-RUN-OPEN`

Two rehearsals ran on the desk against the fake node (no network for the sends), with 2-minute steps for BASE, the reference, the template probe and RETURN (`STORM_LANE_MIN=2`, `STORM_RET_MIN=2`), the cap test at its full 10 minutes (`STORM_CAP_MIN=10`), and the probe's full read capped at 5,000 entries.

- `p21-a`, 2026-11-13 09:17:04Z to 09:46:28Z. Preflight passed; `BUDGET_CHECK` logged (key 0 49,612 usable, 30 planned family minutes, projected end 26,812, over the line plus margin); genesis 16 of 16; `FEE_SPLIT` floor 100, r150 150, r300 300, r450 450; `LANE_PLAN` as in the plan. The cap path did what the plan says: from 600, 600 to 1,200 to 2,000, four decided minutes at 2,000, `CAP_REACHED` after 6 minutes, back to 150, two decisions (150 to 300 to 600), `FROZEN_ARM` lowered the lane's fee cap on purpose, the lane stopped on that cap (`LANE_CAP`), and the rule froze (`FROZEN reason=lane-stopped:cap`). 2,757 lane submits OK, 0 rejected, 0 lost; `RUNNER_EXIT 0`. One fault found: under the 230-a-minute submit cap the lane paced only 177 to 180 a minute (the pacing bucket dropped the fraction). Fixed in the lane process (commit 8af057a).
- `p21-b`, 2026-11-13 09:48:23Z to 10:18:28Z, on the final files (the same files, by hash after line endings, as the live run and this repo's `tools/desk`: desk runner, lane, counter, probe, template watcher). The template probe now paced 230, 230 (N 15) and 230, 230 (N 30) a minute. The cap path repeated: 600 to 1,200 to 2,000, four decided minutes at 2,000, `CAP_REACHED`, 150 to 300 to 600, `FROZEN_ARM`, `LANE_CAP`, `FROZEN reason=lane-stopped:cap`. 2,957 lane submits OK, 0 rejected, 0 lost. The template watcher wrote 565 rows. Every step file, TIMELINE, MEMPOOL and METHOD published to the rehearsal's local origin; no `ERROR` line; `RUNNER_EXIT 0`.
- The fake node does not model block space or fee priority, so the landing numbers above say nothing about the network. They only show that the controller, the cap guard and the freeze run as written.

## Status after the live run

Void. The desk and the Mini lost internet from about 10:25Z to 10:33Z (a robot vacuum knocked the network switch); the reference and the template probe landed almost nothing and the cap test never started. Stopped by `logs/FAILED.md` at 10:35:00Z on the operator's instruction; nothing sent. Lane 207 accepted, 0 rejected, 320.40 tKAS fees (7.76 parked); families about 196 tKAS. See [logs/LESSONS.md](logs/LESSONS.md). Rerun as [pre-run 22](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-22).

### Public statement

We run our own heavy lane on TN10 in this pre-run, with the operator's OK: 8, 15 and 30 chains at a fixed 460 for 6 minutes, then 8 chains for 10 minutes at rates our rule sets between 150 and the 2,000 sompi/gram cap, about five of them at 2,000. While it runs, other TN10 users' transactions paying up to about the lane's rate wait longer on the nodes that see them. In this run the lane landed only 207 transactions before it was stopped (the network outage); its effect on other users was too small and too disturbed to read. This is our own testing; tKAS has no value.

## When something breaks

Append a worked fix to [locks/LOCKED.md](locks/LOCKED.md) in the form that page shows, and a repair line to `logs/FIXES.md`. If the run dies before RETURN, write `logs/FAILED.md`, stop every runner, waiter, and counter, and do not resume. The next attempt is a new repo that starts from this repo's lock file.
