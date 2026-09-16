# UK & European Broker Fee Dataset

Open data on what retail investment platforms actually charge — commissions,
currency-conversion (FX) fees, withdrawal fees, inactivity fees and platform
fees — across 23 brokers available to UK and European investors.

Maintained by [FeesWizard](https://feeswizard.com), an independent fee-comparison site edited
by Yaniv Barshaf, CPA. Every figure is taken from the platform's own published
fee schedule and carries a verification date and source URL.

## Files

| File | Rows | Description |
|---|---|---|
| `broker-fees.csv` / `.json` | 23 | One row per broker: headline fees, regulators, regions, verification date and source |
| `fee-changes.csv` | 9 | Dated log of verified pricing changes (what changed, when, and the source) |

## Column dictionary (broker-fees)

| Column | Meaning |
|---|---|
| `slug` | Stable identifier used in FeesWizard URLs |
| `asset_type` | `investing` (real share ownership) or `cfd` (leveraged contracts) |
| `regions` | Where retail clients can open an account (`uk`, `eu`, `us`), pipe-separated |
| `fx_fee_pct` | Currency-conversion fee, percent per converted trade |
| `withdrawal_fee` | Flat fee per withdrawal, in `plan_currency` |
| `inactivity_monthly` | Monthly dormancy charge, in `plan_currency`, normalised from quarterly/annual charges |
| `platform_fee_pct` | Ongoing annual platform fee as a percent of holdings (first tier, where tiered) |
| `monthly_fee` | Fixed monthly subscription, if any |
| `*_text` | The human-readable fee wording, including conditions the numbers cannot capture |
| `verified_at` | Date the figures were last checked against the source |
| `source_url` | Primary source used for verification |

## Caveats

- **Empty is not zero.** In the numeric fee columns, `0` means we confirmed the
  platform levies no such charge; an empty cell means the fee is not modelled as a
  number for that broker — typically a spread-priced CFD broker with no per-plan
  pricing. Those brokers may still charge: always read the matching `*_text`
  column before treating an empty cell as free. For example `inactivity_monthly`
  is empty for Plus500, AvaTrade and Fortrade, all of which do charge dormancy fees
  described in `inactivity_text`.
- Percentage fees are currency-neutral; flat fees are in the plan's own currency.
- CFD and spread-based brokers price through the spread, so their costs are **not**
  directly comparable with share-dealing commissions. Filter on `asset_type`.
- Fees change. Check `verified_at` and the
  [fee-change tracker](https://feeswizard.com/broker-fee-changes/) before relying on a figure.
- This is factual pricing data, not investment advice. Capital at risk.

## Licence & attribution

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — free to use, including
commercially, with attribution (the same licence as the GitHub and Kaggle mirrors):

> Broker fee data from FeesWizard — https://feeswizard.com

Suggested citation:

> FeesWizard (2026). *UK & European Broker Fee Dataset*. Yaniv Barshaf, CPA. https://feeswizard.com/uk-broker-fee-index/

## Related

- [UK Broker Fee Index](https://feeswizard.com/uk-broker-fee-index/) — the quarterly data study built on this dataset
- [Fee change tracker](https://feeswizard.com/broker-fee-changes/) — verified pricing changes as they happen
- [Methodology](https://feeswizard.com/methodology/) — how figures are collected and verified
