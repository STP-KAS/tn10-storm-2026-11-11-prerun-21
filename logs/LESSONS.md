# Pre-run 21: lessons (void run)

> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · Kaspa Testnet-10 only; tKAS has no value.

**Pre-run 21 is void.** It opened, rehearsed and armed normally (PRE-RUN-OPEN 10:21:17Z, Mini armed 10:21:41Z, desk live from 10:23:00Z). From about 10:25Z to 10:33Z the desk and the Mini lost their internet connection: a robot vacuum knocked the network switch they share. In that window the desk's lane process could not reach its node, the families stopped attempting, the counter marked every minute as lagging, and the step files could not be pushed (BASE, HOLD-1 and HOLD-2 reached origin together at 10:33Z, on the eighth retry). The reference and the template probe therefore landed almost nothing (lane submits a minute: 0, 8, 0, 0, 7, 0, 15), and the cap test held at 600 for want of a reference. On the operator's instruction we published `logs/FAILED.md` at 10:35:00Z; the desk runner, the Mini runner and the bot waiter stopped on it. The bot sent nothing.

So these minutes say nothing about the network, and there are no findings from this run. The same plan runs again as [pre-run 22](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-22).

## What we take from it

- Both nodes were back in sync within minutes (read-only check at 10:38Z: desk and Mini synced, 9 and 8 peers, newest block under a second old, DAA moving about 11 a second).
- The runner noticed only in hindsight: its minute checks waited behind the stuck pushes. Pre-run 22 adds a cheap connectivity guard on its own timer: if, for 2 closed minutes in a row while the lane should run, the lane gets no submit accepted or none of its transactions lands on the desk counter, the runner stops everything (no sends) and publishes `FAILED`.
- The offline rehearsals (p21-a, p21-b) found and fixed one real fault before the open: under a submit cap of 230 a minute the lane paced only 177–180; with the fix it paced 230.

## Spend

- Lane: 207 transactions accepted, 0 rejected, 0 lost, 320.40 tKAS of fees, 7.76 parked on our own sink key (not swept).
- Families: 1,841 hops (floor 414, r150 447, r300 483, r450 497); about 196 tKAS of fees, estimated at pre-run 20's fee a hop for each tier.
- Before the open: housekeeping and the refill of key 0 (all between our own keys, none rejected) about 21 tKAS of fees; calibration a few tKAS.
- About 540 tKAS in all. Key 0 afterwards: 47,546 usable tKAS (part of the drop since the open is the sixteen genesis coins now held in the covenants); the payment pile 679 coins, 13,447 tKAS.
