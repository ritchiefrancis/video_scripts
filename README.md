# FileThat — Tutorial Video Scripts & Deliverables

One folder per video, named `<number>_<video_heading>`. Each folder holds:

- `README.md` — the brief and a tick-off checklist for that video
- `script.html` — the full shot-by-shot script (download and open in any browser), once written
- the finished video files, once delivered

**How we track progress:** tick the checklist in each video's `README.md` as stages complete. The table below is the at-a-glance view.

## Recording order

**Record in numerical order (or whatever order suits the edit).** The old three-batch split existed because the HMRC screens couldn't be staged outside a live quarter — that constraint is gone: every HMRC endpoint is mocked (demo dataset in `filethat/hmrc_mock_endpoints.md`; how to run it in `filethat/DEMO_STAGING.md`). The only per-video gate now is its script being written.

| # | Video | Tier | Script | Notes |
|---|-------|------|--------|-------|
| [1](1_what_is_filethat/) | What is FileThat? | 1 | ✅ | |
| [2](2_set_up_your_account/) | Set Up Your Account | 1 | — | Exists; re-record only if screens changed |
| [3](3_organisation_setup/) | Organisation Setup | 1 | — | Exists |
| [4](4_connecting_to_hmrc/) | Connecting to HMRC | 1 | — | Exists |
| [5](5_your_weekly_5_minutes/) | Your Weekly 5 Minutes | 1 | ✅ | The habit video; quarterly-update shot shared with #1 and #7 — record once, reuse |
| [6](6_your_self_assessment_year/) | Your Self Assessment Year | 1 | ✅ | The journey video; script locked |
| [7](7_submitting_a_quarterly_update/) | Submitting a Quarterly Update | 1 | ✅ | |
| [8](8_cis_getting_your_deductions_back/) | CIS: Getting Your Deductions Back | 1 | ✅ | |
| [9](9_filing_a_vat_return/) | Filing a VAT Return | 1 | ✅ | 🔁 re-record (screens changed); new script written |
| [10](10_bank_statements_and_csv_import/) | Bank Statements & CSV Import | 2 | ✅ | |
| [11](11_digital_records_receipts/) | Digital Records — Receipts | 2 | ✅ | Possible merge with #5 |
| [12](12_paying_hmrc_and_what_you_owe/) | Paying HMRC & What You Owe | 2 | ✅ | |
| [13](13_year_end_extras/) | Year-End Extras | 2 | ✅ | |
| [14](14_nothing_to_report_this_quarter/) | Nothing to Report This Quarter | 2 | ✅ | |
| [15](15_hand_your_books_to_your_accountant/) | Hand Your Books to Your Accountant | 2 | ✅ | |
| [16](16_income_and_expenditure_ledger/) | Income & Expenditure Ledger | 2 | ✅ | 🔁 re-record (screens changed); sibling of #15 — same staged ledger, shoot 15 first, then 16's live add |
| [17](17_mileage_tracking/) | Mileage Tracking | 2 | ✅ | 🔁 re-record (screens changed); no seeding — one trip added live to an empty page; record in its own scene load (the live sync adds a Travel record) |
| [18](18_compliance_checklist/) | Compliance Checklist | 2 | ✅ | 🔁 re-record (screens changed); demo scene 18 stages the mid-year state (1/4 quarters) |
| [19](19_landlords_uk_property_quarterly/) | Landlords: UK Property Quarterly | 3 | ✅ | |
| [20](20_creating_and_sending_an_invoice/) | Creating & Sending an Invoice | 3 | ✅ | |
| [21](21_tax_planner/) | Tax Planner | 3 | ✅ | |
| [22](22_your_dashboards/) | Your Dashboards | 3 | ✅ | |
| [23](23_adding_and_switching_organisations/) | Adding & Switching Organisations | 3 | — | Exists |
| [24](24_amending_after_youve_declared/) | Amending After You've Declared | 3 | ✅ | |
| [25](25_landlords_foreign_property/) | Landlords: Foreign Property Quarterly | 3 | ✅ | New — fully mocked (Costa Blanca Apartment demo data) |

## Open items — tackle when the video comes up

| When | Item |
|------|------|
| Before recording #5 / #11 | Decide the **#5 + #11 merge** (combined ~2:00 receipts cut vs two videos). Both scripts carry the merge note. |
| Before recording #8 | Decide whether the **£1,090 CIS deduction** threads into the calculation + SA-account fixtures as tax-already-paid (changes figures in #6/#12 shots) or stays statement-only. #8's script currently keeps it off the calculation shot. |
| Staging #13 (SE version only) | **Self-employment annual submission GET** is the one unmocked endpoint (returns `{}`). #13 is scripted around the staged UK-property allowances instead; lift the sandbox payload if the SE screen is wanted. |
| ~~Staging #14~~ | ~~Done~~ — loading demo scene 14 now flips WireMock itself (SE cumulative GET 404s, so the update form is genuinely empty); loading any other scene restores the staged figures. |
| Edit of #12, #13 | Both run ~4–5s over 1:00; the **line to trim to caption** is flagged in each script's footer. |
| Before recording sessions (optional) | **`obligation_snapshot_uq` race** logs a benign WARN on first concurrent capture — small retry-on-conflict fix available if clean logs are wanted. |
| Optional tidy-up | Test user's stored HMRC Business Id is `XBIS12345678901`; fixtures use `XAIS12345678910`. Fallback stubs cover it, but aligning via the org settings screen removes the one visible inconsistency. |
| After the shoot | **Remove the deprecated Plaid integration** (`PlaidService`, the Link connect flow in `BankingService`/`OpenBankingController`, and the UI connect pages). Sync now skips CSV-import connections, but live-bank sync still points at Plaid sandbox. |
| After the shoot | **Revert prod**: restart `filethat-api` with `docker_prod_env.txt`, remove `filethat-wiremock` (steps in `filethat/DEMO_STAGING.md`). Don't re-enable registration before reverting. |
| After the shoot | **Revert `minStart={2025}`** back to `2026` on the Tax Calculations page (`new_ui/.../tax_calculations/index.js`, lowered for #6), Your Filing Deadlines (`new_ui/.../in-year/obligations/index.js`, #13's four-fulfilled-quarters shot) and Year-End Allowances (`new_ui/.../self_assessment/annual/index.js`, #13's £420 worked example) — the pickers were lowered so they can reach the staged 2025-26 year (MTD ITSA has no real pre-2026-27 years). |

## Practicalities (all videos)

- 1080p minimum, 16:9, MP4. Clean voiceover mix; VO as a separate stem if possible; SRT captions appreciated.
- British English throughout. The audience is non-tax-savvy — friendly, plain-spoken, no jargon.
- All demo screens and data are staged and recorded by Ritchie before each session; the scripts are the edit and VO guide.
- Where a script has a **fixed claims** section, please keep that wording exactly as written.
