# OMOP AU ETL Tutorial

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

- [`data/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-etl-tutorial/tree/main/data)  
  Example source datasets:
  - NMDS APC-like data: [`apc_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-etl-tutorial/blob/main/data/apc_data.csv)
  - PLIDA PBS-like data: [`plida_pbs_data.csv`](https://github.com/Australian-Health-Data-Evidence-Network/omop-etl-tutorial/blob/main/data/plida_pbs_data.csv)

- [`fig/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-au-etl-tutorial/tree/main/fig)  
  Images used in documentation and presentations.

- [`materials/`](https://github.com/Australian-Health-Data-Evidence-Network/omop-etl-tutorial/tree/main/materials)  
  Contains intermediate outputs from the ETL design process (e.g., WhiteRabbit scan reports, mapping files, documentation).

- [`docs/Security`](https://github.com/Australian-Health-Data-Evidence-Network/omop-etl-tutorial/tree/main/docs/Security/)  
  Contains an example template for a **Third-Party Application Security Assessment (TPASA)** covering tools required during the Pre-ETL stage (e.g., WhiteRabbit and Rabbit-In-a-Hat). The template is provided as a reference and should be adapted to align with your organisation’s cybersecurity policies, risk management framework, and application whitelisting procedures before requesting approval to use OHDSI tools.




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

`Open these pages (Ctrl/Cmd + Click to open in a new tab for your convenience):`

- OpenJDK: [`https://adoptium.net/`](https://adoptium.net/temurin/releases?version=25&mode=filter&os=any&arch=any)   
- Oracle Java: [`https://www.oracle.com/java`](https://www.oracle.com/java/technologies/downloads/)
# Verify Java Installation

After installing Java, verify the installation by running command:

```bash
java -version
```

You should see a version number **≥ 1.8**.

---

# 🪟 Windows

## Step 1 — Open Command Prompt

Choose one of the following:

**Option A (Quickest)**  
- Press `Win + R`  
- Type `cmd`  
- Press `Enter`

**Option B**  
- Click **Start**
- Search for **Command Prompt**
- Open it

**Option C (Terminal or PowerShell also works)**  
- Search for **PowerShell** or **Terminal**
- Open it

---

## Step 2 — Run

```bash
java -version
```

### Expected Output Example

```bash
java version "1.8.0_381"
Java(TM) SE Runtime Environment
```

or

```bash
openjdk version "25.0.2" 2026-01-20 LTS
OpenJDK Runtime Environment Temurin-25.0.2+10 (build 25.0.2+10-LTS)
OpenJDK 64-Bit Server VM Temurin-25.0.2+10 (build 25.0.2+10-LTS, mixed mode, sharing)
```

If the version is **1.8 or higher**, you're good to go.

---

### If You See This Error

```bash
'java' is not recognized as an internal or external command
```

This means:
- Java is not installed, **or**
- Java is not added to your system `PATH`

You will need to install Java and ensure it is added to `PATH`.

---

# 🍎 macOS

## Step 1 — Open Terminal

- Press `Command + Space`
- Type `Terminal`
- Press `Enter`

OR  

Go to:

Applications → Utilities → Terminal

---

## Step 2 — Run

```bash
java -version
```

If Java is not installed, macOS may prompt you to install it automatically.

---

# 🐧 Linux (Ubuntu / Debian)

## Step 1 — Open Terminal

- Press `Ctrl + Alt + T`
OR
- Search for **Terminal** in your applications menu

---

## Step 2 — Run

```bash
java -version
```

---

## If Java Is Not Installed

Install OpenJDK:

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

Then verify again:

```bash
java -version
```

---

# Acceptable Java Versions

Any of the following are valid:

- `1.8.x`
- `11`
- `17`
- `21`
- `25`
- `As long as it is **1.8 or higher**, your setup is correct.`

## 2. Download WhiteRabbit and Rabbit-In-A-Hat

`Open these pages (Ctrl/Cmd + Click to open in a new tab for your convenience):`

Download the latest release from the official OHDSI repository:
[`https://github.com/OHDSI/WhiteRabbit`](https://github.com/OHDSI/WhiteRabbit)

### How to Find the Release File

1. Open the repository link above.
2. On the right-hand side of the page, look for the **Releases** section.
   - It is usually located in the right sidebar.
3. Click on **Releases**.
   - Alternatively, you can go directly to:
    [`https://github.com/OHDSI/WhiteRabbit/releases`](https://github.com/OHDSI/WhiteRabbit/releases)

4. Click the latest release (top-most version).
5. Under **Assets**, download the `.zip` file.
6. Extract the downloaded file to a local directory of your choice (e.g., `C:\WhiteRabbit` or `~/WhiteRabbit`).

---

## 3. Run the Tools

After downloading and extracting the WhiteRabbit release `.zip` file, you will see a folder structure similar to:

```
WhiteRabbit/
├── bin/
├── repo/
└── ...
```

You will run the tools from inside the extracted folder.

---

# WhiteRabbit

## 🪟 Windows

### Step 1 — Open the Extracted Folder

1. Navigate to the folder where you extracted WhiteRabbit.
2. Open the `bin` folder.

### Step 2 — Run the Batch File

Double-click:

```
whiteRabbit.bat
```

WhiteRabbit should now launch.

---

## 🍎 macOS / 🐧 Linux

### Step 1 — Open Terminal

Navigate to the extracted WhiteRabbit folder.

Example:

```
cd /path/to/WhiteRabbit
```

### Step 2 — Make Script Executable (First Time Only)

```
chmod +x bin/whiteRabbit
```

### Step 3 — Run WhiteRabbit

```
./bin/whiteRabbit
```

WhiteRabbit should now launch.

---

# Rabbit-In-A-Hat

Rabbit-In-A-Hat is run the same way.

---

## 🪟 Windows

### Option 1 — Double Click

Inside the `bin` folder, double-click:

```
rabbitInAHat.bat
```

---

## 🍎 macOS / 🐧 Linux

### Step 1 — Navigate to Folder

```
cd /path/to/WhiteRabbit
```

### Step 2 — Make Executable (First Time Only)

```
chmod +x bin/rabbitInAHat
```

### Step 3 — Run

```
./bin/rabbitInAHat
```

---

# Common Issues

### "java is not recognized"
Java is not installed or not added to PATH.

### Permission denied (macOS/Linux)
Run:
```
chmod +x bin/whiteRabbit
chmod +x bin/rabbitInAHat
```

---


# Notes

- These tools are developed and maintained by OHDSI.
- This repository does not redistribute binaries.
- Always use the latest official release.
- Ensure Java is installed before launching the tools.
