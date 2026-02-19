# omop-au-etl-tutorial
Example tutorials and reference materials showing how APC-like and PBS-like datasets can be mapped to the OHDSI OMOP Common Data Model (CDM) using WhiteRabbit and Rabbit-In-A-Hat.

# Background

This repository contains:



## Repository organisation

The repository is generally organised as follows:

* the top level contains the summary information, e.g., the summary presentation [PLACE PRESENTATION LINK HERE]
    + [`fig/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/fig) contains the images used in these documents
* [`data/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/data) contains the data files:
    + the NMDS APC-like data [`apc_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/blob/main/data/apc_data.csv)
    + the PLIDA PBS-like data [`plida_pbs_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/blob/main/data/plida_pbs_data.csv)
* [`materials/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/materials/WhiteRabbit) contains the interim output from the ETL process files 
* [`tools/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/tools) copies of OHDSI tools available freely but included for convenience

And the final directory:


# General process

1. Chuck the [`data/apc_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/blob/main/data/apc_data.csv) and [`data/plida_pbs_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/blob/main/data/plida_pbs_data.csv) csvs through [WhiteRabbit / Rabbit in a Hat ](https://github.com/OHDSI/WhiteRabbit)
2. Use SQL/R code to match the concepts to the `OHDSI Standardized Vocabularies`
3. Put the remaining concepts in the data not matched above through [Usagi](https://github.com/OHDSI/Usagi) to perform "manual matching" (although Usagi and new LLM based tools makes it much easier)
4. Convert (ETL) your data to the OHDSI CDM.
5. Examining Achilles and Data Quality Dashboard output on ARES or ATLAS-Dashboard