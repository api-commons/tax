# Tax

The common tax vocabulary -- the tax calculations made on a sale, the transactions committed for reporting, the jurisdictions and rates that apply, the exemption certificates that waive tax and the filings that report it -- distilled from the APIs that already exist. Payroll taxes belong to the payroll context. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Tax, Tax Compliance, Sales Tax, VAT, Tax Automation, Indirect Tax, E-Invoicing, Tax Calculation in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| tax_calculation | 6 | 5 | tax_amount 60% | calculations 3, calculate 3 |
| tax_transaction | 12 | 11 | id 82%, amount 64%, date 55%, type 55% | transactions 11, refunds 2, orders 1 |

Cohort: 51 providers with harvested OpenAPI, 13 crosswalks. Of the providers exposing a tax_calculation: 83% create, 17% list, 0% fetch, 0% update, 0% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A tax transaction agrees on id, amount, date and type -- the committed record a tax engine reports from.
- A tax calculation agrees on nothing: sales-tax engines, VAT services and global tax APIs each take addresses, lines and exemptions in their own shape, and return a breakdown in another.
- Tax is thin as published OpenAPI (51 providers, 15 mapped), and splits by country -- US sales tax, EU VAT and the UK's Making Tax Digital are three different vocabularies.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Payroll and contractor tax belong to payroll; property-transfer tax quotes are excluded.
- Calculations are `/tax-calculations` and committed transactions `/tax-transactions`: payments and banking own the bare words.
- Rates, exemption certificates and filings were measured and dropped.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
