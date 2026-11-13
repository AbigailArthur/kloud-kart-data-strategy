# Memo to Nana

**From:** Abigail Arthur  
**Date:** 12 November 2026  
**Subject:** Improving Kloud Kart's Reporting and Data Management

## What I found

Kloud Kart's main challenge is not a lack of advanced technology. It is the way business data is currently collected, shared and managed.

My review identified five important concerns:

1. **Website performance:** Reporting exports run on the same database as the live website. These exports have slowed the website twice, creating a risk for customers and daily operations.
2. **Conflicting reports:** Operations and Finance sometimes report different figures because reporting is rebuilt manually without consistently agreed definitions.
3. **Uncontrolled customer copies:** Marketing works with customer lists containing approximately 300,000 people, but copies and access are not properly tracked.
4. **Customer deletion requests:** There is no verified process showing how customer information is located and deleted when requested.
5. **Limited technical capacity:** The business relies heavily on one PHP/MySQL developer and has no dedicated data engineering team.

## What I built

## What I built

| What you asked for | Status | Evidence |
|---|---|---|
| Understand the current data challenges | Completed | `situation_diagnosis.md` |
| Recommend a data architecture | Completed | `recommendation.md` |
| Provide a 12-month implementation plan | Completed | `roadmap.md` |
| Document key technical decisions | Completed | Five ADR files in `decisions/` |
| Provide a board-level presentation | Completed | `04-board-presentation/Kloud_Kart_Board_Presentation_Final.pptx` |
| Deliver an improvement beyond the brief | Completed | `improvement/improvement.md` and `improvement/Monday_Reporting_Reconciliation_Template.docx` |

## What I recommend

I recommend starting with a second server that receives a copy of the production database. Reporting should run from this separate server so that large exports do not interfere with the live website.

Most business reports should refresh daily. Stock availability should remain connected to the live operational system because outdated stock information can lead to incorrect orders.

I also recommend recruiting a Data Engineer first, followed by a BI and Data Governance Analyst. Together, these roles will improve data reliability, reporting and customer information management.

The first year should focus on protecting website performance, creating consistent reports, controlling customer data and preparing the business for further growth.

## What I could not stand behind

The brief did not include actual database exports, system performance records, report samples or server quotations. Therefore, I could not independently verify:

- The exact differences between Operations and Finance reports.
- The current quality and completeness of the database.
- The locations and number of customer data copies.
- The financial cost of previous website slowdowns.
- The current effectiveness of customer deletion procedures.
- The exact cost of the proposed infrastructure and new hires.

These items should be investigated before final implementation. A privacy professional should also review the company's obligations under Ghana's Data Protection Act, 2012 (Act 843).