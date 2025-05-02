# Estig_tool
Python based program to assist in the Answer File creation to support ESTIG scanning


# **🛠 `estig_tool.py` — STIG Workbook and Answer File Automation Tool**

## **🔍 What It Does**

This Python tool helps **automate** and **simplify** the STIG compliance lifecycle by:

* Initializing Excel workbooks for tracking STIG items across products.

* Updating Excel with "Not Reviewed" vulnerabilities from `.cklb` JSON output files.

* Automatically generating **STIG-compliant XML answer files** used by tools like Evaluate-STIG.

* Producing **human-readable Markdown reports** from `.cklb` findings.

* Supporting a fully **interactive CLI** and **modular flag-based interface** for automation.

## **⚙️ Core Use Cases**

1. **Create and manage a centralized Excel workbook** for multiple STIGs and systems.

2. **Auto-import vulnerability keys (V-keys)** marked as `Not_Reviewed` from `.cklb` scan files.

3. **Generate valid XML answer files** that map to the DISA Evaluate-STIG schema.

4. **Clear and reinitialize** workbooks when beginning a new assessment cycle.

5. **Report open findings** across systems and generate a Markdown summary.

---

## **🧩 How It Works**

### **🔢 Command-Line Flags**

| Flag | Description |
| ----- | ----- |
| `-i`, `--init` | Create a new workbook from a template and generate tabs per STIG |
| `-c`, `--clear` | Clear data rows from all STIG sheets in the workbook |
| `-u`, `--update` | Import new “Not Reviewed” V-keys from `.cklb` JSON scans |
| `-m`, `--manualestig` | Legacy alias for `--update` |
| `-g`, `--generate` | Generate XML answer files per STIG using workbook data |
| `-r`, `--report` | Build a Markdown summary from multiple `.cklb` scan files |

Example:

```
python estig_tool.py -c -u -g
```

---

## **📁 Directory Workflow Example**

```
📂 /stig-assessments/
├── 📄 estig_tool.py
├── 📄 template.xlsx          # Excel template with correct headers
├── 📂 scans/
│   ├── SQL2016DB_20240401-121212.cklb
│   ├── RHEL9_20240401-123456.cklb
├── 📂 workbook/
│   └── my_stig_tracking.xlsx
├── 📂 xml_output/
│   └── SQL2016DB.xml
├── 📂 reports/
│   └── stig_report.md
```

---

## **🧪 Step-by-Step Usage**

### **1\. 🔧 Initialize Workbook**

```
python estig_tool.py -i
```

You’ll be prompted to provide:

* A path to your Excel **template**.

* A **destination file** for the new workbook.

Creates one sheet per STIG shortname and adds the “AnswerKey Name” column.

---

### **2\. 🧹 Clear Existing Data**

```
python estig_tool.py -c
```

Deletes all data rows (retains headers) — useful before importing new findings.

---

### **3\. 🚨 Update from `.cklb` Scans**

```
python estig_tool.py -u
```

Prompts:

* Directory of `.cklb` files.

* “ValidTrueComment” (e.g., `STIG COMPLIANT`)

* Whether to also generate XML.

It:

* Extracts “Not Reviewed” V-keys.

* Adds them to Excel if not already present.

* Optionally updates XML answer files for those V-keys.

✅ Maintains only the *latest* scan per STIG using filename timestamps.

---

### **4\. 📤 Generate XML Answer Files**

```
python estig_tool.py -g
```

For each STIG sheet:

* Generates or updates an XML file with `<Vuln>` and `<AnswerKey>` nodes.

* Preserves prior data and appends comments noting added keys.

AnswerKey structure:

```
<AnswerKey Name="DEFAULT">
  <ExpectedStatus>Not_Reviewed</ExpectedStatus>
  <ValidationCode />
  <ValidTrueStatus>NotAFinding</ValidTrueStatus>
  <ValidTrueComment>STIG COMPLIANT</ValidTrueComment>
  ...
</AnswerKey>
```

---

### **5\. 📊 Generate a Markdown Report**

```
python estig_tool.py -r
```

*   
  Scans recursively for `.cklb` files.

* Aggregates findings per host and per STIG.

* Outputs `stig_report_YYYYMMDD-HHMMSS.md` with stats like:

```
### File: SQL2016DB_20240401-121212.cklb
- Host: SERVER01
  - STIG: SQL2016DB — **45** findings
    - Not Reviewed: 20
    - Open: 25

## STIG Implementation Summary
- Total Evaluated: 100
- Compliant (Not a Finding): 70
- Non-compliant (Open): 30
**Overall Implementation: 70.00%**
```

---

## **✅ Why This Tool Is a Good Thing**

### **🔄 Automates a Tedious Process**

STIG compliance normally requires manually copying V-keys and tracking implementation in spreadsheets and XML. This tool removes hours of manual labor.


You get:

* Versioned XMLs with timestamped comments.

* Markdown reports for meetings, ATOs, or POA\&M updates.

### **📚 Interoperability**

Generates valid XML for **Evaluate-STIG**, which integrates with DoD vulnerability management pipelines.

---

## **🔧 Prerequisites**

Install Python dependencies:

```
pip install openpyxl pandas
```

Python 3.13 recommended.

---
