# Bulgarian Localization Ecosystem for Odoo 18 & 19

> **Cross-repo overview** of the full Bulgarian-localization stack — ~115 modules across 5 repositories (Odoo 18 for CE / OCA / expert / enterprise; the EE add-ons are maintained on **both the 18.0 and 19.0 branches**) covering accounting, payroll, banking, NRA/NSI/NOI integration, fiscal printers, payments, and AI-assisted document processing.

## Quick stats

| Repo | Scope | Modules | License model |
|---|---|---|---|
| [`l10n-bulgaria`](https://github.com/rosenvladimirov/l10n-bulgaria) | Community Edition — open-source core | 36 | LGPL-3 / AGPL-3 |
| [`l10n-bulgaria-oca`](https://github.com/OCA/l10n-bulgaria) | OCA-compatible mirrors of CE modules | 25 | LGPL-3 |
| [`l10n-bulgaria-ee`](https://github.com/rosenvladimirov/l10n-bulgaria-ee) | Enterprise add-ons (payroll, NRA decls, InfoPay, …) | 40 | OPL-1 (paid) |
| [`l10n-bulgaria-expert`](https://github.com/rosenvladimirov/l10n-bulgaria-expert) | Specialized expert modules | 10 | OPL-1 |
| [`l10n-bulgaria-enterprise`](https://github.com/rosenvladimirov/l10n-bulgaria-enterprise) | Odoo Enterprise add-ons (ECB rates, license, VAT) | 4 | OPL-1 |
| **Total** | | **~115** | |

## How the repos relate

```
                        ┌────────────────────┐
                        │   l10n-bulgaria    │  CE core (LGPL/AGPL)
                        │   (36 modules)     │
                        └──────────┬─────────┘
                                   │ depends on / extends
        ┌──────────────────────────┼──────────────────────────┐
        │                          │                          │
┌───────▼────────┐  ┌──────────────▼──────────┐  ┌────────────▼──────────────┐
│ l10n-bulgaria- │  │  l10n-bulgaria-ee       │  │  l10n-bulgaria-expert     │
│ oca (25)       │  │  (40 OPL-1)             │  │  (10 OPL-1)               │
│ OCA variants   │  │  Payroll, NRA decls,    │  │  InfoPay variants, VAT    │
│                │  │  InfoPay, contracts     │  │  Art. 69/82, MRP, time-   │
│                │  │                          │  │  machine                  │
└────────────────┘  └──────────────┬──────────┘  └───────────────────────────┘
                                   │
                          ┌────────▼────────────┐
                          │ l10n-bulgaria-      │
                          │ enterprise (4)      │
                          │ Odoo Enterprise     │
                          │ add-ons (ECB rates, │
                          │ license, VAT)       │
                          └─────────────────────┘
```

## Functional groupings (cross-repo)

### Core / Foundation
- **l10n-bulgaria/l10n_bg_config** — central configuration backbone, UIC validation, encryption, mixin architecture
- **l10n-bulgaria/partner_multilang** — JSONB-based multilingual partner names with transliteration
- **l10n-bulgaria/l10n_bg_multilang** — multi-language support for Partner/Company/Employee
- **l10n-bulgaria/l10n_bg_address_extended** — precise BG address formatting
- **l10n-bulgaria/l10n_bg_city** — ЕКАТТЕ geographic database (28 regions, 265 municipalities, 5000+ settlements)
- **l10n-bulgaria/l10n_bg_tax_offices** — NRA territorial directorate registry

### Geographic / Reference data sync
- **l10n-bulgaria/l10n_bg_city.l10n.bg.ekatte.sync** — quarterly cron + dbfread parser for НСИ EKATTE updates (Phase 4.1)
- **l10n-bulgaria-enterprise/l10n_bg_customs_currency_rate_live** — ECB MRO daily rate (Phase 4.3)

### Accounting & Reporting
- **l10n-bulgaria/l10n_bg_reports_audit** — SQL views + NRA tags foundation
- **l10n-bulgaria/l10n_bg_reports_config** — configuration UI for accounting reports
- **l10n-bulgaria/l10n_bg_report_theme** — section-based professional report layout
- **l10n-bulgaria/l10n_bg_invoice_copy** — ОРИГИНАЛ/КОПИЕ watermark
- **l10n-bulgaria/l10n_bg_invoice_grif** — Гриф field on invoice reports
- **l10n-bulgaria-ee/l10n_bg_gfo_reports_ee** — ГФО (NSI Annex 1) financial statements via account.report engine
- **l10n-bulgaria-ee/l10n_bg_intrastat** — Intrastat XML declarations
- **l10n-bulgaria-ee/l10n_bg_assets** — BG tax depreciation rules
- **l10n-bulgaria-ee/l10n_bg_account_reports_patch** — partner-name aggregation fix
- **l10n-bulgaria-ee/l10n_bg_stock_price_diff** — stock valuation difference accounting
- **l10n-bulgaria-enterprise/l10n_bg_report_vat** — advanced VAT report

### Banking & Payments
- **l10n-bulgaria/l10n_bg_bank_wallet** — PBKDF2+Fernet encrypted credential storage
- **l10n-bulgaria/l10n_bg_account_statement_import_mt940** — MT940 bank statement import
- **l10n-bulgaria/l10n_bg_account_reconcile_patch** — partner-name regexp_matches fix for JSONB
- **l10n-bulgaria/payment_borica** — Borica APGW (CGI v4.0, EMV 3DS 2.x)
- **l10n-bulgaria/payment_mypos** — myPOS Checkout API (REST + 3DS)
- **l10n-bulgaria/l10n_bg_infopay** — Borica InfoPay PSD2 core (statement sync, payments)
- **l10n-bulgaria-ee/l10n_bg_infopay_ui** — InfoPay UI wizard
- **l10n-bulgaria-ee/l10n_bg_infopay_ee_payment** — direct EE payment-order submission (BGN/EUR/budget)
- **l10n-bulgaria-ee/l10n_bg_infopay_ee_statement** — bypass OdooFin via Enterprise online sync
- **l10n-bulgaria-expert/l10n_bg_infopay_oca_statement** — OCA bridge to online.bank.statement.provider
- **l10n-bulgaria-expert/l10n_bg_infopay_oca_payment** — OCA bridge to account.payment.order
- **l10n-bulgaria-expert/l10n_bg_infopay_online** — online banking integration

### HR & Payroll
- **l10n-bulgaria/l10n_bg_hr_holidays** — 61 Bulgarian leave types per КТ + НЗОК + чл. 37а НРВПО (Phase 5.1 calendar schedule view, pro-rata helpers, DOO treatment)
- **l10n-bulgaria/l10n_bg_payroll_classifications** — НКПД (occupational) + КИД (economic activity) classifications
- **l10n-bulgaria-ee/l10n_bg_hr_payroll** — main BG payroll w/ DOO/ЗО/УПФ/ТЗПБ, ДДФЛ, МОД, КТ compliance
- **l10n-bulgaria-ee/l10n_bg_hr_payroll_holidays** — sick leave + NSSI cert auto-creation + чл. 37а notice
- **l10n-bulgaria-ee/l10n_bg_hr_payroll_account** — accounting integration
- **l10n-bulgaria-ee/l10n_bg_hr_payroll_extended** — payslip input collection from any model
- **l10n-bulgaria-ee/l10n_bg_hr_payroll_garnishment** — court order garnishment per BG CPC art. 446 (¼/⅓/½/¼ cap matrix)
- **l10n-bulgaria-ee/l10n_bg_hr_contract_sign** — electronic signature integration
- **l10n-bulgaria-ee/l10n_bg_2026_hr_payroll** — 2026 МРЗ/МОД/rates dataset

### Non-employment regimes
- **l10n-bulgaria-ee/l10n_bg_civil_contract** — civil contract under ZZD art. 258-264 (25% normative deduction, ZO threshold)
- **l10n-bulgaria-ee/l10n_bg_management_contract** — management contract (ДУК) under TZ art. 244
- **l10n-bulgaria-ee/l10n_bg_self_insured** — self-insured persons under KSO art. 4 par. 3
- **l10n-bulgaria-ee/l10n_bg_cooperator_contract** — cooperative member regime
- **l10n-bulgaria-ee/l10n_bg_chl_114_contract** — casual day-worker under KT art. 114 (5 days / 40h max per month)
- **l10n-bulgaria-ee/l10n_bg_hr_a1_form** — A1 posted-worker certificate for EU/EEA/Switzerland (Phase 3.1 + 3.2 legislation mapper, 31 countries)

### NRA Declarations & APIs
- **l10n-bulgaria/l10n_bg_api_nra** — NRA REST API core (OAuth 2.0, D1/D6/ETZ/VAT, NAP standalone app)
- **l10n-bulgaria-ee/l10n_bg_api_nra_dec1** — Декларация Обр. 1
- **l10n-bulgaria-ee/l10n_bg_api_nra_dec6** — Декларация Обр. 6
- **l10n-bulgaria-ee/l10n_bg_api_nra_etz** — Електронен трудов записник (ТД чл. 62)
- **l10n-bulgaria-ee/l10n_bg_api_nra_vat** — VAT declaration
- **l10n-bulgaria-ee/l10n_bg_api_nra_noi** + `_d1` + `_d6` — НОИ form variants
- **l10n-bulgaria-ee/l10n_bg_account_nra_vat** — ДДС ZIP package generator
- **l10n-bulgaria-ee/l10n_bg_hr_payroll_nra_dec1** — payroll → Obr.1 (EMPL2026.TXT)
- **l10n-bulgaria-ee/l10n_bg_hr_payroll_nra_etz** — payroll → ETZ
- **l10n-bulgaria-ee/l10n_bg_hr_payroll_nra_noi** — payroll → НОИ Обр. 1+6

### External integrations
- **l10n-bulgaria/l10n_bg_company_registry** — Trade Registry API (portal.registryagency.bg)
- **l10n-bulgaria/l10n_bg_tariff_code** — TARIC/HS/CN codes + EU API
- **l10n-bulgaria/taric_ai_classifier** — AI (Claude)-powered TARIC classification

### Fiscal Printers (ErpNet.FP)
- **l10n-bulgaria/l10n_bg_erp_net_fp** — fiscal printer integration
- **l10n-bulgaria/l10n_bg_erp_net_fp_fleet** — central fleet manager
- **l10n-bulgaria/l10n_bg_erp_net_fp_iot_oca** — CE/OCA iot bridge
- **l10n-bulgaria-ee/l10n_bg_erp_net_fp_iot** — EE iot.box bridge

### AI / OCR / pipeline
- **l10n-bulgaria/l10n_bg_ai_pipeline** — pipeline stack with progressive-disclosure skills
- **l10n-bulgaria-ee/l10n_bg_ai_invoice_glue** — vendor bill AI extraction (composite OCR + vision)
- **l10n-bulgaria-ee/l10n_bg_ai_customs_glue** — customs declaration AI extraction

### Configuration plugins
- **l10n-bulgaria-ee/l10n_bg_config_plugins_nsi_expences** — NSI expense chart of accounts
- **l10n-bulgaria-ee/l10n_bg_config_plugins_payroll** — social-security contribution accounts
- **l10n-bulgaria-expert/l10n_bg_config_plugins_art_69_2** — VAT Act art. 69 par. 2 plugin
- **l10n-bulgaria-expert/l10n_bg_config_plugins_art_82_2** — VAT Act art. 82 par. 2 plugin

### Tax administration
- **l10n-bulgaria-expert/l10n_bg_tax_admin** — fiscal positions, customs protocols, VAT protocols
- **l10n-bulgaria-expert/l10n_bg_tax_admin_manual** — manual tax-admin corrections

### MRP / specialized
- **l10n-bulgaria/l10n_bg_mrp_multilang** — multi-language MRP workcenter names
- **l10n-bulgaria/l10n_bg_project_multilang** — multi-language project task fields
- **l10n-bulgaria-expert/mpr_costs_quantity** — piece-rate MRP costing
- **l10n-bulgaria-expert/odoo_time_machine** — temporary state rollback

### Stock / Sale extensions
- **l10n-bulgaria/l10n_bg_report_stock** — accepted delivery documents in stock picking
- **l10n-bulgaria/l10n_bg_sale_order_delivery_note** — delivery report for SO
- **l10n-bulgaria/l10n_bg_stock_picking_comment_template** — comment-template repositioning
- **l10n-bulgaria/l10n_bg_stock_sale_line_description** — SO line desc on pickings

### Licensing
- **l10n-bulgaria-ee/l10n_bg_license_client** + `_server` — internal license management
- **l10n-bulgaria-enterprise/l10n_bg_license_client` + `_server` — Enterprise variants

### Multi-installation / MCP
- **l10n-bulgaria/l10n_bg_claude_terminal** — Claude Code terminal + AI Tokenizer (Qdrant/Ollama)
- **l10n-bulgaria-ee/l10n_bg_claude_installations** — manage multiple MCP installations

### Patches / shims
- **l10n-bulgaria/hr_org_chart_multilang_fix** — JSONB name resolution for hr_org_chart widget
- **l10n-bulgaria/l10n_bg_account_reconcile_patch** — partner name regexp_matches fix
- **l10n-bulgaria/markdown_viewer_locale** — localized Markdown viewer

## Architectural conventions

- **Mixin pattern:** `l10n.bg.config.mixin` for field visibility; `res.transliterate.mixin` for transliteration; `l10n.bg.infopay.statement.mixin` / `payment.mixin` for InfoPay bridges; `l10n.bg.packaging.weighable.mixin` for ErpNet.FP weighable items
- **JSONB translations:** PostgreSQL JSONB columns for multilingual fields (names, descriptions); regexp queries must handle this
- **Encryption layers:** XOR+Base64 (config secrets), PBKDF2+Fernet (`bank_wallet`, InfoPay tokens)
- **API integration:** OAuth 2.0 (NRA), REST with caching (TARIC), direct (Trade Registry), HMAC-signed (Borica payments)
- **Plugin architecture:** Chart of accounts templates, config plugins (art. 69/82, NSI expenses, payroll)
- **Report sections:** Header/Article/Footer with XPath inheritance (`l10n_bg_report_theme`)
- **Field-naming convention:** `l10n_bg_` prefix mandatory for fields added to Odoo core models by any localization module
- **Dual reporting modules:** `l10n_bg_reports_audit` (CE) and `l10n_bg_vat_reports` (EE) define the same `_name` — enterprise wins on load order
- **Layered tagging on `account.move.line`:** NRA tags propagated through stored compute graph

## Dependency hierarchy (simplified)

```
Level 1: l10n_bg → l10n_bg_config → partner_multilang → l10n_bg_multilang
Level 2: l10n_bg_city → l10n_bg_tax_offices → l10n_bg_company_registry
Level 3: l10n_bg_bank_wallet → l10n_bg_infopay → bridge modules (oca/ee)
Level 4: l10n_bg_api_nra → declaration sub-modules
Level 5: l10n_bg_report_theme → l10n_bg_reports_audit → l10n_bg_reports_config
Level 6: l10n_bg_tariff_code → taric_ai_classifier
Level 7: l10n_bg_hr_holidays + l10n_bg_payroll_classifications → l10n_bg_hr_payroll
Level 8: l10n_bg_hr_payroll → contract-type extensions + NRA payroll declarations + garnishment + A1
```

## Installation order (clean DB)

For a from-scratch installation, install in this order:

1. **Foundation:** `l10n_bg`, `l10n_bg_config`, `partner_multilang`, `l10n_bg_multilang`, `l10n_bg_address_extended`
2. **Geographic:** `l10n_bg_city`, `l10n_bg_tax_offices`
3. **Banking primitives:** `l10n_bg_bank_wallet`, `l10n_bg_account_statement_import_mt940`
4. **Reports foundation:** `l10n_bg_report_theme`, `l10n_bg_reports_audit`, `l10n_bg_reports_config`
5. **NRA API core:** `l10n_bg_api_nra`
6. **Trade Registry + TARIC:** `l10n_bg_company_registry`, `l10n_bg_tariff_code`
7. **HR baseline:** `l10n_bg_hr_holidays`, `l10n_bg_payroll_classifications`
8. **Payroll (EE):** `l10n_bg_hr_payroll`, `l10n_bg_hr_payroll_holidays`, `l10n_bg_hr_payroll_account`
9. **Non-employment regimes (EE, as needed):** `l10n_bg_civil_contract`, `l10n_bg_management_contract`, `l10n_bg_self_insured`, `l10n_bg_cooperator_contract`, `l10n_bg_chl_114_contract`, `l10n_bg_hr_a1_form`
10. **NRA declarations (EE):** `l10n_bg_api_nra_dec1`, `_dec6`, `_etz`, `_vat`, then payroll-driven wrappers
11. **Banking integration:** `l10n_bg_infopay` + bridges (OCA expert OR EE)
12. **Specialized add-ons** as needed (assets, intrastat, GFO reports, AI extraction, payment providers)

## Documentation map

| Topic | Where |
|---|---|
| **This ecosystem overview** | `claude.ai/L10N_BG_ECOSYSTEM.md` (knowledge repo) |
| Each module README (EN) | `<repo>/<module>/README.en.md` or `README.md` (vendor-handwritten) |
| Each module README (BG) | `<repo>/<module>/README.bg.md` |
| Odoo 18 → 19 deltas (EE) | per-module `## Odoo 18 → 19 differences` section in each EE README (19.0 branch) |
| Per-repo overview | `<repo>/OVERVIEW.md` + `OVERVIEW.bg.md` (and repo-root `README.md`) |
| Memory / project knowledge | `claude.ai/memory/*.md` |
| Roadmaps | `claude.ai/memory/project_payroll_personnel_roadmap_2026_05_13.md` etc. |
| Installation guide | `claude.ai/memory/installation_guide_bg.md` |
| Reference (paths, APIs) | `claude.ai/memory/reference_repo_paths.md` |

## Licensing summary

- **Open-source (LGPL-3, AGPL-3):** all `l10n-bulgaria` modules + `l10n-bulgaria-oca` (61 modules, free)
- **Commercial (OPL-1):** `l10n-bulgaria-ee` (40 modules), `l10n-bulgaria-expert` (10 modules), `l10n-bulgaria-enterprise` (4 modules) — paid license required for production

## Maintainer

Rosen Vladimirov — Bulgarian Odoo developer & consultant, 11+ years on l10n_bg. Issues, questions, and commercial inquiries via GitHub on each repo's issue tracker.

---

*Last refreshed 2026-05-16. Deep-analysis README campaign **complete** across all 5 repos: l10n-bulgaria / -oca / -expert / -enterprise (18.0) hand-quality READMEs pushed; l10n-bulgaria-ee — 18.0 branch already canonical, 19.0 branch given a full code-verified v19 deep pass (`ad87cf1`, 35 modules, each with an "Odoo 18 → 19 differences" section). Per-repo OVERVIEW.md/.bg.md present on all repos (ee: 18.0 branch). See `claude.ai/memory/MEMORY.md` for the living knowledge index.*
