# Domain Knowledge: Financial Services — Investment Management & Market Data

Domain-specific content for financial services solution management. Commands and agents reference this file for identifiers, NFR defaults, regulatory requirements, failure modes, and validation flags.

This file reflects the domain of systematic investment management firms (custom indexing, overlay strategies, tax-managed portfolios) and the market data infrastructure that supports them.

## Financial Instrument Identifiers

| Identifier | Scope | Format | Example |
|------------|-------|--------|---------|
| CUSIP | US/Canada | 9 chars (6 issuer + 2 issue + 1 check) | 037833100 |
| ISIN | Global | 12 chars (2 country + 9 local + 1 check) | US0378331005 |
| SEDOL | UK/Ireland | 7 chars alphanumeric | 2046251 |
| FIGI | Global | 12 chars (BBG prefix) | BBG000B9XRY4 |
| Ticker | Exchange-specific | Variable | AAPL |
| RIC | Reuters | Variable with suffix | AAPL.OQ |

**Cross-reference rule:** Any canonical instrument record should carry at least ISIN + one local identifier. Flag records with only a ticker — tickers are not globally unique.

## Investment Management Concepts

### Portfolio Construction & Management

| Concept | Definition |
|---------|-----------|
| Direct indexing | Owning individual securities to replicate an index, enabling tax-loss harvesting and customization at the account level |
| Overlay strategy | Managing exposures (currency, duration, beta) across accounts without changing underlying holdings |
| Tax-loss harvesting (TLH) | Selling positions at a loss to offset gains, replacing with correlated substitutes to maintain exposure |
| Wash sale rule | IRS rule prohibiting repurchase of substantially identical security within 30 days before/after a loss sale |
| Custom indexing | Building bespoke benchmarks with client-specific exclusions (ESG screens, concentrated stock, sector tilts) |
| Model portfolio | Target allocation template applied across many accounts with account-level customization |
| Drift / rebalancing | Deviation from target weights triggering trade generation to restore alignment |
| Sleeve | Sub-allocation within an account managed by a specific strategy or manager |
| Transition management | Moving a portfolio from one strategy/manager to another while minimizing cost and tax impact |
| Completion portfolio | Filling gaps in a client's total exposure by building around existing concentrated positions |

### Account Structures

| Structure | Description |
|-----------|------------|
| SMA (Separately Managed Account) | Individual account with direct security ownership, full tax customization |
| UMA (Unified Managed Account) | Single account with multiple sleeves/strategies managed as one |
| Model delivery | Centralized model distributed to sponsor platforms (Schwab, Fidelity, Pershing) |
| Household | Group of related accounts managed for aggregate tax efficiency |
| Taxable vs tax-deferred | Different optimization rules: taxable accounts prioritize TLH, IRAs/401k ignore wash sales |

### Order Management & Trading

| Concept | Definition |
|---------|-----------|
| Trade generation | Algorithmic process comparing current holdings to target model, producing orders |
| Block trading | Aggregating orders across accounts for better execution, then allocating fills |
| Pre-trade compliance | Checking proposed trades against restrictions before execution |
| Post-trade compliance | Verifying executed trades meet all restrictions after settlement |
| Restriction | Account-level rule: do-not-buy, do-not-sell, sector cap, ESG screen, concentrated stock hold |
| Cash management | Maintaining target cash levels, investing inflows, raising cash for outflows/fees |
| Lot selection | Choosing which tax lots to sell (highest cost, FIFO, specific ID) to optimize tax outcome |

## Market Data NFR Defaults

Starting-point NFR values for market data and portfolio management systems.

| Quality | Target | Conditions | Measurement |
|---------|--------|------------|-------------|
| Latency (real-time pricing) | p99 < 500ms | Market hours, streaming feeds | APM traces |
| Latency (batch pricing) | < 15 min from market close | End-of-day pricing | Job completion logs |
| Latency (trade generation) | < 5 min per 10k accounts | Rebalance run | Job duration logs |
| Data freshness | < 1 min for actively traded instruments | During market hours | Staleness monitor |
| Price accuracy | 99.99% match to exchange source | All instrument types | Recon vs exchange feed |
| Availability | 99.95% during market hours | Trading days only | Uptime dashboard |
| Tax lot accuracy | 100% match to custodian records | All accounts | Daily custodian recon |
| Lineage | Full provenance from source to consumer | All data points | Lineage graph query |
| Auditability | 7-year retention, immutable audit trail | All price changes, trade decisions | Audit log query |
| Throughput (rebalance) | 50k accounts in < 30 min | Monthly full rebalance | Job metrics |
| Throughput (market data) | 100k updates/sec sustained | Peak market volatility | Load test |

## SAFe / PI Planning Terminology

| Term | Definition |
|------|-----------|
| PI (Program Increment) | 8-12 week planning cycle, typically 4-5 sprints + IP sprint |
| ART (Agile Release Train) | Long-lived team of teams (50-125 people) |
| RTE (Release Train Engineer) | Facilitator for the ART |
| Feature | ART-level deliverable, fits within one PI |
| Capability | Solution-level deliverable spanning multiple ARTs |
| Enabler | Technical infrastructure or exploration work |
| PI Objective | SMART goal committed by a team for the PI |
| WSJF | Weighted Shortest Job First — prioritization (CoD / Job Size) |
| IP Sprint | Innovation and Planning sprint at end of PI |

## Regulatory Requirements

| Regulation | Jurisdiction | Key Requirements |
|-----------|-------------|-----------------|
| SEC Rule 204 / Reg SHO | US | Locate and deliver requirements for short sales |
| Investment Advisers Act | US | Fiduciary duty, best execution, trade allocation fairness |
| SOX | US | Financial reporting controls, audit trail, data integrity |
| ERISA | US | Prudence and diversification requirements for retirement accounts |
| Reg NMS | US | National best bid/offer, order protection rule |
| GDPR | EU | Personal data handling in client-facing analytics |
| MiFID II | EU | Best execution, transaction reporting, data transparency |
| Dodd-Frank | US | OTC derivatives reporting, swap data repositories |
| BCBS 239 | Global | Risk data aggregation, accuracy, completeness, timeliness |
| IRS wash sale rules | US | 30-day window for substantially identical securities |

**Compliance flags for requirements review:**
- Does this feature handle client PII? → GDPR / privacy review required
- Does this feature affect trade execution or allocation? → Best execution / fairness review
- Does this feature produce client reports or performance numbers? → GIPS / SOX controls review
- Does this feature touch tax lot or cost basis data? → IRS reporting accuracy review
- Does this feature aggregate risk data? → BCBS 239 compliance review
- Does this feature involve retirement accounts? → ERISA fiduciary review
- Does this feature generate trades across accounts? → Fair allocation review (no cherry-picking)

## Common Failure Modes

Flag these during data model review, NFR definition, and architecture decisions:

| Failure Mode | Description | Detection | Mitigation |
|-------------|------------|-----------|------------|
| Stale pricing | EOD prices not updated, yesterday's close used for rebalance | Staleness monitor, timestamp check | Alerts on missing updates, fallback hierarchy |
| Wash sale violation | TLH sells a position that was bought within 30-day window in another account in the household | Pre-trade wash sale check across household | Cross-account wash sale engine, 30-day lookback |
| Duplicate trades | Same rebalance generates orders twice due to incomplete job state | Idempotency check on rebalance run ID | Idempotency keys, rebalance state machine |
| Restriction violation | Trade generated that violates account-level restrictions (ESG screen, do-not-buy) | Pre-trade compliance engine | Restriction check in trade generation pipeline |
| Missing corporate actions | Stock splits, dividends not applied to positions before rebalance | CA calendar vs applied actions recon | Daily CA completeness check before rebalance |
| Identifier mismatch | Same instrument with different IDs across custodians and internal systems | Cross-reference validation | Golden source identifier mapping (FIGI preferred) |
| Drift miscalculation | Drift calculated on stale prices or missing positions | Price age check + position completeness check | Staleness gate before drift calculation |
| Tax lot mismatch | Internal tax lot records diverge from custodian records | Daily custodian tax lot reconciliation | Automated recon with break resolution workflow |
| Model-to-account mismatch | Target model updated but not propagated to all accounts | Model version tracking vs account version | Model version propagation with confirmation |
| Cash drag | Uninvested cash sitting in accounts eroding performance | Cash balance monitoring vs target cash | Automated cash sweep / invest rules |
| Holiday calendar gaps | Rebalance runs on exchange holidays (no prices to use) | Holiday calendar validation | Exchange-specific calendar integration |
| Stale reference data | Instrument metadata (sector, country, currency) outdated causing misclassification | Age check on reference data | Periodic refresh from vendor, change detection |

## Financial Services Validation Flags

When reviewing any artifact, check for these investment-management-specific concerns:

- **Multi-asset coverage** — Does the solution handle equities, fixed income, ETFs, derivatives, alternatives? Flag if only single-asset.
- **Account-level customization** — Can the system apply different rules per account (restrictions, tax status, cash targets)?
- **Household awareness** — Does the system see across accounts in a household for wash sale checks and tax coordination?
- **Tax status handling** — Does it distinguish taxable, tax-deferred (IRA), tax-exempt (Roth) and apply different logic?
- **Custodian integration** — Which custodians (Schwab, Fidelity, Pershing, BNY)? File formats? Reconciliation cadence?
- **Model vs account distinction** — Is there a clear separation between the target model and individual account holdings?
- **Lot-level tracking** — Does the system track individual tax lots with purchase date, cost basis, and holding period?
- **Corporate actions** — How are stock splits, mergers, dividends, spinoffs, delistings handled at the lot level?
- **Settlement cycles** — T+1 (US equities), T+2 (international), T+0 (treasuries) — is settlement aware?
- **Vendor dependency** — Bloomberg, Refinitiv, ICE, FactSet, index providers (MSCI, S&P, FTSE) — which vendors? SLA terms? Failover?
- **Golden source** — Is there a single source of truth for pricing, positions, restrictions, and models?
- **Scalability** — Can it handle 50k+ accounts in a single rebalance run?
- **Audit trail** — Can every trade decision be traced back to the model, the drift trigger, the lot selection logic, and the restriction check?
