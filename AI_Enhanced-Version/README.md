
# **ESTIG Tool** – Enhanced STIG Management with AI-Powered PowerShell Generation

A comprehensive Python tool for managing **Security Technical Implementation Guide (STIG)** compliance with **AI-powered PowerShell validation code generation**.

---

## 🚀 Features

### **Core STIG Management**
- **Initialize Workbooks** – Create Excel workbooks from templates for STIG tracking
- **Update from Scans** – Import `Not_Reviewed` V-keys from `.cklb` scan files
- **Generate XML** – Create XML answer files from Excel workbooks
- **Generate Reports** – Build comprehensive Markdown reports from `.cklb` files
- **Clear Data** – Clean existing workbook data

### **AI-Enhanced PowerShell Generation**
- **STIG Library Parser** – Extract rules from official STIG ZIP files
- **AI Code Generation** – Generate PowerShell validation scripts using local AI models
- **Multiple AI Support** – Compatible with Ollama, LM Studio, and OpenAI-compatible APIs
- **Interactive Selection** – Browse and select specific STIG rules for code generation
- **File Export** – Save generated code as `.ps1` or `.txt` files

---

## 📋 Requirements

### **Python Dependencies**

```pip install openpyxl pandas requests```


### **Option 1: LM Studio**

1. Download and install LM Studio
2. Download a code generation model (e.g., CodeLlama, Deepseek Coder)
3. Start the local server in LM Studio
4. Note the server URL (typically `http://localhost:1234`)

### **STIG Library (Optional)**

* Download official STIG ZIP files from the [DISA STIG Library](https://public.cyber.mil/stigs/)
* Extract them to a directory for parsing

---

## 🛠 Installation

1. Clone or download the `estig_tool_ai.py` file
2. Install dependencies:

   ```
   pip install openpyxl pandas requests
   ```
3. Set up your AI model in LM Studio or other supported AI server
4. Configure the tool:

   ```
   python estig_tool_ai.py -a
   ```

**Configuration prompts:**

* **Base URL** – Your AI server endpoint (e.g., `http://localhost:1234`)
* **Model Name** – The AI model to use (e.g., `codellama`, `deepseek-coder`)
* **Timeout** – Request timeout in seconds (default: 120)
* **Output Directory** – Where to save generated PowerShell files

Example `ai_config.json`:

```
{
  "base_url": "http://localhost:1234",
  "model": "deepseek-coder-6.7b-instruct",
  "timeout": 200,
  "output_dir": "./generated_powershell"
}
```

---

## 🖥 Usage

### **Command Line Interface**

```
# Configure AI settings
python estig_tool_ai.py -a

# Generate PowerShell from STIG library
python estig_tool_ai.py -l

# Manual PowerShell generation
python estig_tool_ai.py -p

# Traditional STIG operations
python estig_tool_ai.py -u    # Update from scans
python estig_tool_ai.py -g    # Generate XML
python estig_tool_ai.py -r    # Create reports
```

### **Interactive Menu**

Run without arguments:

```
python estig_tool_ai.py
```

---

## 📚 STIG Library Usage

### 1. Prepare STIG Library

```
mkdir stig_library
cd stig_library
```

Download STIG ZIP files from DISA. Example:

```
stig_library/
├── U_MS_Windows_10_V2R8_STIG.zip
├── U_MS_Windows_Server_2019_V3R2_STIG.zip
└── U_Active_Directory_Domain_V3R6_STIG.zip
```

### 2. Parse and Generate Code

```
python estig_tool_ai.py -l
```

The tool will:

* Scan the library directory for ZIP files
* Parse XCCDF files to extract STIG rules
* Display available STIGs and rules
* Generate PowerShell validation code for selected rules
* Save code with descriptive headers and metadata

---

## 🤖 AI-Generated Code Structure

Example generated script:

```
# PowerShell STIG Validation Script
# Generated: 2025-01-15 10:30:45
# STIG: Windows Server 2019 Security Technical Implementation Guide
# Rule: V-253467 - Windows Server 2019 must have the built-in guest account disabled
# Severity: MEDIUM
#
# Description:
# The built-in guest account is a potential security risk...
# ============================================================================

$ValidationResults = [PSCustomObject]@{
    Results = ""
    Valid   = $true
}

try {
    $GuestAccount = Get-LocalUser -Name "Guest" -ErrorAction SilentlyContinue
    if ($GuestAccount -and $GuestAccount.Enabled) {
        $ValidationResults.Results = "❌ Guest account is enabled - STIG violation"
        $ValidationResults.Valid = $false
    } else {
        $ValidationResults.Results = "✅ Guest account is disabled - STIG compliant"
    }
} catch {
    $ValidationResults.Results += "Error: $($_.Exception.Message)`n"
    $ValidationResults.Valid = $false
}

return $ValidationResults
```

---

## 📖 Detailed Usage Example

**STIG Library Workflow**


# 1. Configure AI
```python estig_tool_ai.py -a```

# 2. Browse STIG library
```python estig_tool_ai.py -l```
```
```# Enter path: C:\STIG_Library
# Select STIG: Windows Server 2019
# Select rule: V-253467
# Generated code is displayed and optionally saved
```

---

## 🗂 File Structure

```
project-directory/
├── estig_tool_ai.py           # Main application
├── ai_config.json             # AI configuration (auto-generated)
├── generated_powershell/      # Generated PowerShell files
│   ├── Windows_Server_2019_V_253467_20250115_103045.ps1
│   └── Active_Directory_V_243467_20250115_104322.ps1
└── stig_library/              # STIG ZIP files (optional)
    ├── U_MS_Windows_Server_2019_V3R2_STIG.zip
    └── U_Active_Directory_Domain_V3R6_STIG.zip
```



## 🔧 Troubleshooting

### **AI Connection Issues**



**Common causes:**

* Wrong base URL (check AI server address)
* Model not loaded
* Firewall blocking connection
* AI server not running

### **STIG Library Issues**

* No ZIP files found – ensure files are in the correct directory
* No rules extracted – verify ZIP contains valid XCCDF XML
* Parsing errors – check that ZIP files are not corrupted

---

## 💡 Performance Tips

* Increase timeout for complex STIG rules (e.g., `200+` seconds)
* Use smaller models for quicker generation
* Close other applications to free up system resources

---

## 🤝 Supported STIG Types

* **Operating Systems:** Windows 10/11, Windows Server 2016/2019/2022, RHEL, Ubuntu
* **Applications:** Microsoft Office, Adobe Products, Web Browsers
* **Services:** Active Directory, DNS, IIS, SQL Server
* **Network Devices:** Cisco routers and switches
* **Security Tools:** Microsoft Defender, Trellix ENS

---

## 📝 Contributing

To extend or modify the tool:

* Add new AI providers → `generate_powershell_code()`
* Support new formats → Modify the XCCDF parsing functions
* Add validation types → Enhance the AI prompt templates
* Improve error handling → Add specific error cases

---

## ⚖ License

This tool is provided *as-is* for STIG compliance management.
Ensure compliance with your organization’s policies when using AI-generated code.
**Always review AI-generated PowerShell before use in production environments.**

---

## 🔗 Resources

* [DISA STIG Library](https://public.cyber.mil/stigs/)
* [Ollama Documentation](https://ollama.ai/)
* [LM Studio](https://lmstudio.ai/)
* [STIG Viewer](https://public.cyber.mil/stigs/stig-viewing-tools/)

```
```
