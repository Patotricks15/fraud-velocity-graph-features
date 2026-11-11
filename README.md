# fraud-velocity-graph-features (FD04)

**Status: blocked.** No verified real dataset with card and device IDs is available yet, so this repository holds the plan and the data requirements only. No analysis code and no synthetic data are included, by design.

**Question:** Do velocity and shared-entity features add signal beyond the baseline?

## Planned method

- Velocity features per entity: `velocity_k(card, t) = count(tx where time in (t - k, t])` and the matching sums, for `k` = 1 hour, 24 hours and 7 days. Computed on sorted data with a strict `shift`, so no feature uses the current transaction.
- Time features: hour, weekday, and time since the previous transaction on the same card.
- Graph features: connected components (networkx) over shared-device or shared-merchant edges between accounts.
- Evaluation: ablation table with baseline, baseline plus velocity, and baseline plus velocity plus graph features. Time-ordered split 70/15/15, PR-AUC as the primary metric.

## Blocking issue

- The Credit Card Fraud Detection dataset (`mlg-ulb/creditcardfraud`) has anonymized PCA features and no card or device identifiers, so it cannot support entity-level features.
- IEEE-CIS Fraud Detection has card and device IDs and is a real candidate. It is a competition dataset with its own rules, and its data could not be read without authentication (see the portfolio plan, Appendix A). It must be verified before use.
- The project does not proceed on synthetic or generated data.

## Unblock criteria

1. Confirm the dataset's license and terms of use, and record the slug, license, and read date in `data/README.md`.
2. Confirm that card and device identifiers exist and that the time column allows time-ordered splits.
3. Read the data in place in a Kaggle Notebook. It is never downloaded or committed.

## Related

- Plan: `fraud-detection-portfolio-plan.md` (workspace root), rows FD04 and Notes on scope.
