# Sexual Harassment Charges Analysis — Oct. 1995 to Sept. 2016

This repository contains data, analytic code, and findings that support portions of the BuzzFeed News article, "[We Got Government Data On 20 Years Of Workplace Sexual Harassment Claims. These Charts Break It Down](https://www.buzzfeed.com/lamvo/eeoc-sexual-harassment-data?utm_term=.mlLxr4pR7#.reAEQ4VD1)," published Dec. 5, 2017. Please read that article, which contains important context and details, before proceeding.

## Data

### Sexual harassment charges

Anonymized data of sexual harassment charges filed to the [U.S. Equal Employment Opportunity Commission](https://www.eeoc.gov/) (EEOC) were provided by a spokesperson from the commission.

Data includes the following header:

- `CHARGE_FILING_DATE`
- `CP_SEX`
- `CP_NATIONAL_ORIGIN`
- `CP_DOB`
- `HISPANIC_CP`
- `CP_RACE_STRING`
- `R_NAICS_CODE`
- `R_NAICS_DESCRIPTION`
- `R_NUMBER_OF_EMPLOYEES`
- `R_TYPE`

Regarding the data, the following notes were provided by an EEOC spokesperson:  

> CP_National_Origin: We greatly expanded the national origin options in 2008. Prior to that, this field will most likely be blank or “Other National Origin”.

> CP Hispanic_CP: This field is populated with “Y” if the Charging Party has identified themselves as Hispanic but, like the National Origin, this field was added in 2008.

> CP_Race_String: Charging Parties may select multiple races that they identify with. This string includes all selected races as a string of codes. See below for code decryption.
R_Type: This is the basic type of respondent (Private, State/Local Agency, School, etc.)

> Race Codes:

- A — Asian or Pacific Islander - Obsolete
- B — Black or African American
- H — Native Hawaiian or Other Pacific Islander
- I — American Indian or Alaska Native
- N — Unable to Obtain Information from Charging Party
- O — Other Race - Obsolete
- S — Asian
- W — White
- Z — Charging Party Declined to Provide

### Economic data

The industry and sector metrics —  on the total workforce, female workforce, and average hourly earnings — use seasonally-adjusted summary data from the [Bureau of Labor Statistics](https://www.bls.gov) (BLS).

No single BLS dataset contains those metrics for every industry and sector. The numbers were chiefly sourced from the [Current Employment Statistics](https://www.bls.gov/ces/) survey and [Occupational Employment Statistics](https://www.bls.gov/oes/current/oes_stru.htm) program, in that order of preference.

The Current Employment Survey data can be accessed through [this data portal](https://data.bls.gov/cgi-bin/dsrv?ce). The Occupational Employment Statistics data come from the "National industry-specific and by ownership" download [here](https://www.bls.gov/oes/tables.htm), specifically `natsector_M2016_dl.xlsx`.

For one sector (agriculture), workforce gender was sourced from the [Current Population Survey](https://www.bls.gov/cps/cpsaat11.htm).

### NAICS descriptions

NAICS sector descriptions came from the [Census Bureau](https://www.census.gov/cgi-bin/sssd/naics/naicsrch?chart=2017), and were supplemented by [this guide to "NAICS Supersectors" for the CES data](https://www.bls.gov/sae/saesuper.htm).

## Code

This repository uses Python code to process the data. That code can be found in the following two notebooks:

### [`01-merge-bls-data.ipynb`](notebooks/01-merge-bls-data.ipynb)

- Merges the economic data described above, and combines it with the NAICS descriptions
- Merges that data with additional, manually curated information needed for the graphics

### [`02-analyze-eeoc-claims.ipynb`](notebooks/02-analyze-eeoc-claims.ipynb)

- Combines the three separate spreadsheets supplied by the EEOC into one data table
- Aggregates the claims by industry and sector
- Merges the industry aggregates with the economic data described above
- Calculates the gender distribution of EEOC claims, to support this passage: "Overall, 83% of the claims were were filed by women, and 15% by men. The remainder did not specify a gender."
- Generates summary data for the article's graphics: `d3_claims_by_industry.csv` and `d3_claims_by_sector.csv`

## Feedback / Questions?

Contact Lam Thuy Vo at lam.vo@buzzfeed.com.

Looking for more from BuzzFeed News? [Click here for a list of our open-sourced projects, data, and code](https://github.com/BuzzFeedNews/everything).
