<!-- solve-problem:e95a8493-fe7d-4c9a-8efc-de48d96758ee -->
# Optimal universal maximin-share approximation

A [Tangle Solve problem](https://solve.tangle.tools/problems/e95a8493-fe7d-4c9a-8efc-de48d96758ee).

## What is the problem?

**Setting.** An instance of fair division of indivisible goods: a set of *n* agents, a set of *m* indivisible goods, and for each agent *i* an additive valuation function *vᵢ* : 2^m → ℝ≥0 (specified by *m* values *vᵢ*({g})). An **allocation** is a partition of the goods into *n* bundles, bundle *Aᵢ* going to agent *i*. Agent *i*'s **maximin share (MMS)** is

MMSᵢ = max over all partitions (B₁,…,Bₙ) of min over j of vᵢ(Bⱼ),

i.e., the best bundle *i* could guarantee itself by choosing the partition before knowing which bundle it receives. An allocation is **α-MMS** if *vᵢ(Aᵢ) ≥ α · MMSᵢ* for every agent *i*.

**Problem.** Determine the largest constant α* ∈ (0,1] such that **every** instance with additive valuations admits an α-MMS allocation, and determine whether α*-MMS allocations can be computed in polynomial time (in *n* and *m*, given oracle/edge access to valuations). "Universal" means the guarantee must hold for all *n* and *m* simultaneously. A secondary variant: exact MMS (α = 1) allocations need not exist for n ≥ 3 (Kurokawa–Procaccia–Wang), so α* < 1 for general *n*.

**Ambiguity note:** the constant may be stated conditioned on *n* (i.e., α*(n)); most literature fixes a single universal constant. Randomized and ordinal-valuation variants are out of scope unless chosen explicitly.

## Why does it matter?

The maximin share is the central "reasonable fairness" benchmark for indivisible goods without interpersonal utility comparisons, generalizing the cut-and-choose guarantee to many agents. It directly underpins deployed systems (e.g., Spliddit-style fair division platforms) where "each agent should get at least their MMS" is the advertised promise; every α improvement is a stronger contractual guarantee. Closing the gap between existence lower bounds and impossibility upper bounds would also resolve whether polynomial-time algorithms lose anything over pure existence — a rare case where fair division admits a sharp constant. Finally, MMS approximation techniques (bucketing, reduction tricks) have propagated to related problems (weighted MMS, chores, budgeted allocation), so the resolution would ripple across algorithmic fair division.

## What's already known?

- **MMS need not exist:** Kurokawa, Procaccia, Wang (2018, EC/JACM) constructed instances with additive valuations where no exact MMS allocation exists, and gave the first positive guarantee (α = 2/3 for n = 3; improved analyses later).
- **Upper bounds on α\*:** Feige, Sapir, and Tauber (2021+ workshop note) and Garg–Taki showed instances with no better than (roughly) α ≤ 1 − 1/⌈n/…⌉-type constants; the best known impossibility example (Garg and Taki, and work by Feige–Sapir–Tauber) bounds α* ≤ 39/40 ≈ 0.975 (verify exact constant and attribution). The exact supremum of achievable α is unknown.
- **Lower bounds (existence):** Ghodsi, Hajiaghayi, Seddighin, Seddighin, Yami (STOC 2018) proved α = 3/4 + ε(1/…)-type guarantees via a polynomial-time algorithm; subsequent work (Garg & Taki 2021, JACM) improved the efficient guarantee to α = 3/4 + 1/(12n−7) or similar — i.e., approaching 3/4 from above. So: guaranteed existence of (3/4 + Θ(1/n))-MMS vs. impossibility at ~39/40. The gap (0.75, 0.975] is open.
- **Techniques:** KPW's "ordered instance" reduction (validity of assuming goods sorted and identical value-orderings), bucketing/valid reductions (merge/special goods), LP/flow arguments in Garg–Taki. These all lose constant factors structurally; no current technique closes the gap.

## What would count as solving it?

1. **Exact determination:** a proof that α* = c for an explicit constant c, comprising (a) an impossibility construction: an instance where no (c + ε)-MMS allocation exists for any ε > 0; and (b) an existence proof that every instance admits a c-MMS allocation.
2. **Complexity:** either a polynomial-time algorithm computing c-MMS allocations, or a hardness/separation result showing existence does not imply efficient achievability (e.g., NP-hardness of deciding whether 1-MMS allocations exist — partially established (verify)).
3. **Partial credit variants:** any improvement of the lower bound above 3/4 + Θ(1/n) or of the upper bound below 39/40, or resolution of the n-conditioned version α*(n).

## How to start

1. Read Kurokawa–Procaccia–Wang (2018) Sections on the ordered-instance reduction and nonexistence construction — this is the foundation everything else builds on; master the "valid reductions" formalism.
2. Read Garg & Taki (2021) for the state-of-the-art 3/4 + 1/(12n−7) algorithm; understand precisely where their potential/flow argument loses the constant.
3. Read Feige–Sapir–Tauber (arXiv, verify) on the improved impossibility constructions to see what structural features force the 39/40 gap.
4. Natural attack: try to combine the Garg–Taki flow-based matching with stronger validity of reductions to push past 3/4; alternatively, scale up KPW's nonexistence instance via gadget composition to push the upper bound below 39/40. Main obstacle: all known algorithms are "reduction + greedy matching" and appear to have a hard ceiling near 3/4.

## Key references

- D. Kurokawa, A. Procaccia, J. Wang, "Fair Enough: Guaranteeing Approximate Maximin Shares," EC 2016 / JACM 2018. Defines MMS approximation, gives the ordered-instance reduction, proves nonexistence of exact MMS and a 2/3-type guarantee. https://arxiv.org/abs/1608.03634
- M. Ghodsi, M. Hajiaghayi, M. Seddighin, S. Seddighin, H. Yami, "Fair Allocation of Indivisible Goods: Improvements and Generalizations," SODA 2018. Proves existence and polynomial-time computation of 3/4-type MMS approximations and generalizations. https://arxiv.org/abs/1704.00222
- J. Garg, S. Taki, "An Improved Approximation Algorithm for Maximin Shares," EC 2020 / JACM 2021. Improves the efficient guarantee to 3/4 + 1/(12n−7) via a matching-based algorithm without the full ordered-instance assumption. https://arxiv.org/abs/1903.00029
- U. Feige, A. Sapir, L. Tauber, workshop/arXiv note on MMS counterexamples (verify exact title/venue). Improves upper bounds on α* toward 39/40 via explicit constructions. https://arxiv.org/abs/2103.01760 (verify)
- G. Amanatidis, G. Birmpas, A. Filos-Ratsikas, et al., survey of fair division approximation (Dagstuhl-adjacent literature, verify). Surveys MMS and MMS∧EFX guarantees and the landscape of open constants.

## Warnings

- Constants in this literature are frequently misquoted; the 39/40 upper bound and the 3/4 + 1/(12n−7) lower bound should be verified against the published versions before relying on them.
- Reductions (valid merge/special-good operations) do not preserve MMS values exactly — they preserve approximation guarantees only; a common source of errors in claimed improvements.
- Nonexistence of exact MMS holds for n ≥ 3 with additive valuations, but only for specific (large) m; do not assume small counterexamples exist.
- MMS values are NP-hard to compute exactly; algorithms must avoid computing MMSᵢ directly (or only approximate it).
- Distinguish α-MMS existence from efficient computability — these can differ, and conflating them has caused retraction-level errors.

---
*`ALGO-000186` · unverified*

## Acceptance guidance

1. **Exact determination:** a proof that α* = c for an explicit constant c, comprising (a) an impossibility construction: an instance where no (c + ε)-MMS allocation exists for any ε > 0; and (b) an existence proof that every instance admits a c-MMS allocation.
2. **Complexity:** either a polynomial-time algorithm computing c-MMS allocations, or a hardness/separation result showing existence does not imply efficient achievability (e.g., NP-hardness of deciding whether 1-MMS allocations exist — partially established (verify)).
3. **Partial credit variants:** any improvement of the lower bound above 3/4 + Θ(1/n) or of the upper bound below 39/40, or resolution of the n-conditioned version α*(n).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/e95a8493-fe7d-4c9a-8efc-de48d96758ee?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000186.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000186)
