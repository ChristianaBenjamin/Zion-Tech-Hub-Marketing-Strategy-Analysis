# Zion Tech Hub Registration Growth Analysis

Decision-support analysis for Zion Tech Hub's next advertising campaign and Cohort 11 growth plan.

The project combines registration data from Cohorts 9 and 10 to answer two marketing questions:

1. Where should Zion Tech Hub put its first advertising budget, and on which audiences?
2. What should Zion Tech Hub do differently to grow its community and fill Cohort 11?

The analysis focuses on stated discovery channel, registration timing, course preference, country, gender, and occupation where available. The available data records registrations, not paid conversions.

## Company context

Zion Tech Hub provides training and mentorship in data analytics, data science, and artificial intelligence. The company also supports corporate training and data consultancy.

## Executive summary

The registration signal is concentrated in one channel, one recurring demand pattern, and one anchor course family:

- X/Twitter was the dominant stated discovery channel in both cohorts and increased from 62.6% of Cohort 9 registrations to 86.5% of Cohort 10 registrations.
- WhatsApp declined from 18.3% to 2.9%, while LinkedIn declined from 15.1% to 7.0%. These are signals to investigate and instrument, not proof that the channels cannot work.
- Data Science / AI / ML represented 45.6% of registrations in both cohorts after normalizing different source labels.
- Cohort 10 registrations were highly concentrated: 87.1% occurred on Thursday or Friday, 62.0% occurred in the evening, and 48.5% occurred between 17:00 and 20:00.
- Cohort 10 was Nigeria-led. Nigeria represented 62.0% of registrations, followed by Kenya at 11.1%.
- Students were the largest single known occupation group at 19.9%, but the remaining audience was fragmented across business, finance, technology, healthcare, and other roles.
- Course interest was broader than declared occupation. Sales & Marketing represented 19.9% of Cohort 10 course demand but only 1.8% of declared occupations matched that area. Supply Chain represented 6.4% of course demand but only 1.2% of declared occupations matched operations or supply chain.

## Recommended first ad budget

The recommended starting point is an evidence-led test budget of ₦500,000. The amount is an example that makes the split operational; the percentages can be applied to another approved budget.

| Channel or use | Share | Example on ₦500,000 | Role in the test |
| --- | ---: | ---: | --- |
| X/Twitter | 60% | ₦300,000 | Scale the strongest stated registration source. |
| LinkedIn | 25% | ₦125,000 | Test professional audiences and course-led messages. |
| Facebook / Instagram | 10% | ₦50,000 | Controlled test only because organic registration signal is low. |
| Tracking and creative reserve | 5% | ₦25,000 | UTM setup, landing-page variants, and creative testing. |

Within the paid-media portion, test audiences in this order:

1. 45%: Data Science / AI / ML and early-career audiences.
2. 20%: Sales / Marketing and business audiences.
3. 15%: Finance audiences.
4. 10%: Healthcare audiences.
5. 10%: Supply Chain / Operations audiences, especially on LinkedIn.

These are test allocations, not claims of profitability. The source data does not include spend, clicks, cost per registration, payment status, or downstream enrollment, so the first seven days must establish those measures before the next budget tranche is scaled.

## Recommended Cohort 11 actions

1. **Instrument every acquisition link before launch.** Add UTM source, medium, campaign, audience, ad set, and referral code fields to the form or CRM. Add payment status and downstream enrollment status so registration volume is not mistaken for revenue conversion.
2. **Launch mid-week and intensify on Thursday and Friday from 17:00 to 20:00.** This follows the strongest Cohort 10 registration pattern. Use a mid-week announcement, a Thursday reminder, and a Friday last-call message.
3. **Build the referral loop inside WhatsApp.** Give community members a tagged invite link, a simple referral prompt, and a clear reason to share. The Referral channel was small but stable at approximately 2.4% across both cohorts, while WhatsApp's stated share fell sharply.
4. **Use course-outcome creative rather than occupation-only targeting.** Lead with the job or capability outcome of each course. Course demand exceeded the visible matching occupation groups for Sales / Marketing, Healthcare, and Supply Chain, which suggests that exact job-title targeting would miss interested prospects.
5. **Run professional audience tests on LinkedIn.** Test Finance, IT / Technology, Data Analyst, Business / Entrepreneur, procurement, logistics, and operations messages. Keep X/Twitter as the scale channel while LinkedIn identifies higher-intent professional segments.
6. **Use Nigeria as the core market and Kenya as the first geographic expansion test.** Nigeria supplied most Cohort 10 registrations, while Kenya was the next-largest country. Do not assume the pattern generalizes to other countries without additional data.

## Data sources

The source files supplied with the project are:

- `Cohort 9.0 (Responses).xlsx - Form responses 1 (2).csv`
- `Cohort 10.0 Registration form (Responses) - Cohort 10.0 Registration form (Responses).csv`
- `Zion_Tech_Hub_Data_Challenge.docx`, which provides the company and dataset context.

Only Cohorts 9 and 10 were supplied. The brief refers to three cohorts, but no third cohort file was available for this analysis.

Source coverage:

| Cohort | Registration rows | Date range | Occupation field |
| --- | ---: | --- | --- |
| Cohort 9 | 1,147 | 2025-11-06 to 2026-02-04 | Not captured in source |
| Cohort 10 | 171 | 2026-05-06 to 2026-06-04 | Available |
| **Total** | **1,318** | — | — |

## Data preparation

The two source schemas were mapped into one canonical registration table. The cleaned table contains 26 fields, including source provenance and derived timing fields.

### Cleaning rules

1. Read both CSV exports as text to preserve identifiers and source values.
2. Mapped different source headers to common names such as `Name`, `Email`, `Phone`, `Country`, `Course`, and `Channel`.

| Field | Description |
| --- | --- |
| `Cohort` | Cohort label, such as Cohort 9 or Cohort 10. |
| `Cohort Number` | Numeric cohort identifier. |
| `Registration Timestamp` | Parsed registration timestamp. |
| `Registration Date` | Date portion of the timestamp. |
| `Registration Month` | Month key in `YYYY-MM` format. |
| `Registration Week` | Monday-start week key. |
| `Registration Day` | Day of week. |
| `Registration Hour` | Hour extracted from the timestamp. |
| `Registration Period` | Morning, Afternoon, or Evening. |
| `Name` | Standardized name, or `Not captured`. |
| `Email` | Trimmed and lower-case email value. |
| `Phone` | Normalized phone value, or `Not captured`. |
| `Country Source` | Cleaned source country text before canonical mapping. |
| `Country` | Standardized country name. |
| `Country Quality Flag` | Standardized, corrected / standardized, or unknown / invalid. |
| `Gender` | Standardized gender label. |
| `Course` | Standardized source course label. |
| `Course Family` | Comparable course grouping used in the analysis. |
| `Occupation` | Standardized Cohort 10 occupation segment. |
| `Occupation Capture` | Whether occupation was captured, blank in source, or unavailable by design. |
| `Channel` | Standardized stated discovery channel. |
| `Channel Group` | Organic social, Owned / Community, or Referral. |
| `SourceFile` | Original source filename. |
| `SourceRow` | Source row reference used for traceability. |
| `Record Status` | Inclusion status after duplicate review. |
| `Timestamp Parse Status` | Parsed or unparsed timestamp status. |

## Dashboard guide

The Excel workbook contains:

- **Dashboard**: headline registration KPIs, cohort comparisons, channel mix, course preference, timing, occupation mix, budget split, and Cohort 11 actions.
- **Cleaned Data**: one standardized table named `RegistrationData`.
- **Cleaning Log**: transformation rules, assumptions, source differences, duplicate handling, and data-quality notes.

The Power BI project contains one semantic-model table named `Registrations` and a dashboard page with native editable charts for channel, course family, registration day, and registration period.

## Dashboard
![image](https://github.com/ChristianaBenjamin/Zion-Tech-Hub-Marketing-Strategy-Analysis/blob/main/Zion_Tech_Hub_Dashboard.png)
### Opening the Power BI project

1. Download and unzip `Zion_Tech_Hub_Registration_Analysis_PBIP.zip`.
2. Open `Zion_Tech_Hub_Registration_Analysis.pbip` in Power BI Desktop.
3. The model is packaged as a portable cleaned snapshot. The adjacent cleaned CSV can be used as the starting point for a future refresh connection.
4. If a binary `.pbix` is required, open the PBIP project in Power BI Desktop and use **File → Save As**.


## Limitations

This project supports a registration-attribution decision, not a complete marketing performance model. The source data does not include:

- advertising spend or budget by channel;
- impressions, clicks, reach, or frequency;
- UTM parameters, campaign names, ad sets, or referral codes;
- payment status, paid enrollment, revenue, CAC, or retention;
- reliable occupation data for Cohort 9;
- a third cohort, despite the wording of the original brief.

Therefore, channel recommendations should be treated as first-test hypotheses. The next data capture cycle should add attribution and payment fields so the team can optimize on cost per registration and cost per paid enrollment.


## Author
Benjamin Christiana Ifelola
Data Analyst
