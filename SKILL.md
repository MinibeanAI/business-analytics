---
name: business-analytics
description: Analyze operational business data from Excel, CSV, SQLite, or similar sources and produce a decision-oriented, branded interactive HTML dashboard. Use when the user needs business analysis across restaurants, coffee shops, retail, ecommerce, venues, reservations, memberships, services, SaaS, or other transaction businesses; when data comes from Meituan, Youzan, POS, mini-programs, delivery platforms, marketplaces, or multiple systems; or when an existing dashboard must be rebuilt around the user's real business, channels, logo, and brand colors.
---

# Business Analytics

Build the analysis from the user's business model and available evidence. Do not clone one industry's dashboard structure, metrics, wording, or visual style into another industry.

## Workflow

1. Inspect every supplied data file before designing the dashboard. Identify tables, time coverage, grain, keys, monetary fields, status fields, customer identifiers, products or services, channels, stores, refunds, discounts, fees, capacity, and membership fields.
2. Read [routing-and-modes.md](references/routing-and-modes.md) and select the closest business mode. Combine modules when the data spans several modes; omit modules that the data cannot support.
3. Read [input-and-channel-mapping.md](references/input-and-channel-mapping.md). Create a field map and reconcile platform definitions before calculating metrics. Keep source fields traceable.
4. Read [metrics-and-periods.md](references/metrics-and-periods.md). State the metric definitions used, analysis period, comparison period, and any coverage limits.
5. If the user supplies a logo or brand image, read [theme-and-brand.md](references/theme-and-brand.md) and run `python3 scripts/extract_theme.py IMAGE_PATH`. Treat the result as a starting palette; adjust contrast and hierarchy for charts and text. User-specified colors take priority.
6. Design the page using [dashboard-ui.md](references/dashboard-ui.md). Generate one self-contained HTML file that opens from `file://` without a server unless the user requests another format.
7. Validate calculations and interactions using [quality-checklist.md](references/quality-checklist.md). Open the result in a browser and test all tabs, filters, chart tooltips, responsive layouts, and the console.

## Analysis contract

- Use real names, units, date coverage, stores, channels, and business labels from the supplied data. Clearly label simulated data only when the data is simulated.
- Separate source facts, derived metrics, diagnostic inference, and recommended action. Do not present an inferred cause as a recorded fact.
- Reconcile totals before visualization: paid amount, refunds, merchant discounts, platform discounts, delivery charges, commissions, service fees, tax, and settlement may belong to different accounting layers.
- Never fabricate customer identity. Do not merge customers across platforms unless the data contains an explicit shared key. When identifiers are incomplete, show identifiable-customer coverage and limit new/returning and retention analysis to the valid subset.
- Prefer monthly analysis. A single selected month uses compact charts and within-month structure; two or more months show monthly trends, period comparisons, drivers, and cohort changes. Use year-over-year comparison only when matching prior-year months are complete.
- Let users select start month, end month, channel, store, and any domain-specific dimension justified by the data. Keep controls compact and recompute every KPI, chart, conclusion, and recommendation from the same filter state.
- Replace dense detail tables with clear charts, ranked views, and short conclusions. Keep downloadable detail data in a collapsed section only when it is useful.
- End each major tab with conclusions tied to the selected period: what changed, the quantified driver, the business implication, and a concrete next action.

## Output expectations

The default deliverable is a polished decision dashboard, not a data dump. Its information architecture, chart mix, language, and visual character must change with the business mode. Typical tabs include an overview plus only the relevant domain modules, such as products, customers, channels, time and capacity, stores, subscriptions, or operations.

When input quality blocks a metric, keep the page useful: show the available analysis, name the missing field, explain the affected conclusion, and give the smallest data requirement needed to unlock it.
