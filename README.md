# omop-au-etl-tutorial

Example tutorials and reference materials demonstrating how APC-like and PBS-like datasets can be mapped to the OHDSI OMOP Common Data Model (CDM) using WhiteRabbit, Rabbit-In-A-Hat, and associated OHDSI tools.

---

# Background

This repository provides:

- Example APC-like and PBS-like datasets
- WhiteRabbit scan outputs
- Mapping design artefacts
- Supporting materials for demonstrating an OMOP ETL workflow in an Australian context

---

# Repository Organisation

The repository is organised as follows:

- **Top level**
  - Summary documentation and presentation materials  
    *(Add presentation link here once available)*

- [`fig/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/fig)  
  Images used in documentation and presentations.

- [`data/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/data)  
  Example source datasets:
  - NMDS APC-like data: [`apc_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/blob/main/data/apc_data.csv)
  - PLIDA PBS-like data: [`plida_pbs_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/blob/main/data/plida_pbs_data.csv)

- [`materials/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/materials)  
  Contains intermediate outputs from the ETL design process (e.g., WhiteRabbit scan reports, mapping files, documentation).

---

# General Process

The tutorial follows a simplified OMOP ETL workflow:

1. Profile the source data (`apc_data.csv`, `plida_pbs_data.csv`) using  
   **WhiteRabbit** and design the ETL using **Rabbit-In-A-Hat**.

2. Map source concepts to the **OHDSI Standardized Vocabularies** using SQL and/or R.

3. Use **Usagi** for semi-automated vocabulary mapping of remaining unmatched source codes.

4. Implement the ETL to transform the source data into the OMOP CDM structure.

5. Evaluate the resulting OMOP database using:
   - **Achilles**
   - **Data Quality Dashboard**
   - ARES / ATLAS dashboards

---

# WhiteRabbit & Rabbit-In-A-Hat Setup

This tutorial uses official OHDSI tools for source data profiling and ETL design:

- **WhiteRabbit** – scans source data and generates summary statistics  
- **Rabbit-In-A-Hat** – designs the ETL mapping to the OMOP CDM  

These tools are **not distributed in this repository**.  
Please download them directly from the official OHDSI source.

---

## 1. Prerequisites

WhiteRabbit and Rabbit-In-A-Hat require:

- **Java 8 (1.8) or higher**

### Install Java

You may install Java from:

- OpenJDK (recommended): https://adoptium.net/  
- Oracle Java: https://www.oracle.com/java/technologies/downloads/

After installation, verify:

```bash
java -version
```

You should see a version number ≥ 1.8.

---

## 2. Download WhiteRabbit

Download the latest release from the official OHDSI repository:

https://github.com/OHDSI/WhiteRabbit

Steps:

1. Click **Releases**
2. Download the latest `.zip` file
3. Extract to a local directory

---

## 3. Run the Tools

After extracting:

### WhiteRabbit

- **Windows**
  ```
  bin/whiteRabbit.bat
  ```

- **macOS / Linux**
  ```bash
  ./bin/whiteRabbit
  ```

---

### Rabbit-In-A-Hat

- **Windows**
  ```
  bin/rabbitInAHat.bat
  ```

- **macOS / Linux**
  ```bash
  ./bin/rabbitInAHat
  ```

---

# Notes

- These tools are developed and maintained by OHDSI.
- This repository does not redistribute binaries.
- Always use the latest official release.
- Ensure Java is installed before launching the tools.