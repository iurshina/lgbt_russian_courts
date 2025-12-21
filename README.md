## Repository Structure and Data Description

This repository contains court data collected from Russian public judicial databases documenting administrative cases related to LGBT symbols and expression, as well as the notebook used to gather and process this data.

### Files

#### `lgbt_cases_symbols_anonymized.json`

This file contains the **anonymized dataset of administrative court cases related to the public display of LGBT symbols**, primarily prosecuted under Article 20.3 of the Russian Code of Administrative Offenses (display of extremist symbols).

#### `cases_6_21_anonymized.json`

This file contains the **anonymized dataset of administrative court cases related to so-called “LGBT propaganda” provisions**, prosecuted under Article 6.21 of the Russian Code of Administrative Offenses.

**Format**

The file is a JSON array. Each element represents a single court case and includes two main components:

* `metadata`: structured information extracted from the court record, such as:

  * region
  * court name
  * date of decision
  * legal articles cited
  * outcome (fine, arrest, confiscation, etc.)
  * judge (retained)
  * accused (anonymized)

* `case_text`: the full text of the court decision, as published on the official court website, with personal data removed.

This structure allows both **quantitative analysis** (e.g. counts by region or year) and **qualitative analysis** of judicial reasoning and language.

**Anonymization**

All personal data identifying the **accused persons** has been removed from both the structured metadata and the full decision texts. Names of defendants are replaced with a placeholder token (e.g. `[ACCUSED]`). This includes common Russian name variants such as full names and surname–initial combinations.

The names of **judges are intentionally preserved**, as judges act in an official public capacity and their identification is relevant for institutional and legal analysis.

Anonymization was performed programmatically using a combination of:

* structured metadata (where accused names were explicitly listed), and
* targeted text replacement in the decision body, optionally assisted by Russian-language named-entity recognition tools.

This approach balances research transparency with harm reduction, ensuring that individuals targeted by these cases are not further exposed to risk.

---

#### `Gather_court_data.ipynb`

This Jupyter notebook documents the **data collection and preprocessing workflow**.

It demonstrates how court decisions were:

* queried and downloaded from regional court websites,
* parsed into structured fields,
* filtered using keyword searches (e.g. “ЛГБТ”),
* cleaned and normalized for analysis.

The notebook uses **SudrfParser**, an open-source parser developed by Data Out ([https://dataout.org/](https://dataout.org/), [https://github.com/dataout-org/sudrfparser](https://github.com/dataout-org/sudrfparser)). Because the official documentation of the tool did not fully cover all practical use cases, this notebook serves as a **worked example** of how the parser can be applied in real research settings, including handling inconsistencies across court websites.

The notebook is provided to support **reproducibility** and to assist other researchers working with Russian judicial data.