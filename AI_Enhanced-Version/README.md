# ESTIG Tool - Enhanced STIG Management with AI PowerShell Generation

A comprehensive Python tool for managing Security Technical Implementation Guide (STIG) compliance with AI-powered PowerShell validation code generation.

## 🚀 Features

### Core STIG Management
- **Initialize Workbooks**: Create Excel workbooks from templates for STIG tracking
- **Update from Scans**: Import Not_Reviewed V-keys from .cklb scan files
- **Generate XML**: Create XML answer files from Excel workbooks
- **Generate Reports**: Build comprehensive Markdown reports from .cklb files
- **Clear Data**: Clean existing workbook data

### AI-Enhanced PowerShell Generation
- **STIG Library Parser**: Extract rules from official STIG ZIP files
- **AI Code Generation**: Generate PowerShell validation scripts using local AI models
- **Multiple AI Support**: Compatible with Ollama, LM Studio, and OpenAI-compatible APIs
- **Interactive Selection**: Browse and select specific STIG rules for code generation
- **File Export**: Save generated code as .ps1 or .txt files

## 📋 Requirements

### Python Dependencies
Install required packages:
```bash
pip install openpyxl pandas requests

Option 1: LM Studio
Download and install LM Studio
Download a code generation model (e.g., CodeLlama, Deepseek Coder)
Start the local server in LM Studio
Note the server URL (typically http://localhost:1234)
STIG Library (Optional)
Download official STIG ZIP files from DISA STIG Library
Extract to a directory for parsing
🛠️ Installation
Clone or download the estig_tool_ai.py file
Install dependencies: pip install openpyxl pandas requests

Set up your AI model LM Studio
Configure the tool: 

python estig_tool_ai.py -a


You'll be prompted to configure:

Base URL: Your AI server endpoint (e.g., http://localhost:1234 for LM Studio)
Model Name: The AI model to use (e.g., codellama, deepseek-coder)
Timeout: Request timeout in seconds (default: 120)
Output Directory: Where to save generated PowerShell files


{
  "base_url": "http://localhost:1234",
  "model": "deepseek-coder-6.7b-instruct",
  "timeout": 200,
  "output_dir": "./generated_powershell"
}


🖥️ Usage
Command Line Interface


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



Interactive Menu
Run without arguments for the interactive menu:

python estig_tool_ai.py



📚 STIG Library Usage
1. Prepare STIG Library



# Create directory structure
mkdir stig_library
cd stig_library

# Download STIG ZIP files from DISA
# Example structure:
# stig_library/
# ├── U_MS_Windows_10_V2R8_STIG.zip
# ├── U_MS_Windows_Server_2019_V3R2_STIG.zip
# └── U_Active_Directory_Domain_V3R6_STIG.zip



2. Parse and Generate Code


python estig_tool_ai.py -l



The tool will:

Scan the library directory for ZIP files
Parse XCCDF files to extract STIG rules
Display available STIGs and rules
Generate PowerShell validation code for selected rules
Save code with descriptive headers and metadata
🤖 AI-Generated Code Structure
The tool generates PowerShell validation scripts with this structure:



# PowerShell STIG Validation Script
# Generated: 2025-01-15 10:30:45
# STIG: Windows Server 2019 Security Technical Implementation Guide
# Rule: V-253467 - Windows Server 2019 must have the built-in guest account disabled
# Severity: MEDIUM
#
# Description:
# The built-in guest account is a potential security risk...
#
# ============================================================================

$ValidationResults = [PSCustomObject]@{
    Results = ""
    Valid   = $true
}

try {
    # AI-generated validation logic here
    $GuestAccount = Get-LocalUser -Name "Guest" -ErrorAction SilentlyContinue
    
    if ($GuestAccount -and $GuestAccount.Enabled) {
        $ValidationResults.Results = "❌ Guest account is enabled - STIG violation"
        $ValidationResults.Valid = $false
    } else {
        $ValidationResults.Results = "✅ Guest account is disabled - STIG compliant"
        $ValidationResults.Valid = $true
    }
} catch {
    $ValidationResults.Results += "Error: $($_.Exception.Message)`n"
    $ValidationResults.Valid = $false
}

return $ValidationResults



📖 Detailed Usage Examples
Example 1: STIG Library Workflow

# 1. Configure AI
python estig_tool_ai.py -a

# 2. Browse STIG library
python estig_tool_ai.py -l
# Enter path: C:\STIG_Library
# Select STIG: Windows Server 2019
# Select rule: V-253467
# Generated code is displayed and optionally saved











🗂️ File Structure



project-directory/
├── estig_tool_ai.py           # Main application
├── ai_config.json             # AI configuration (auto-generated)
├── generated_powershell/      # Generated PowerShell files
│   ├── Windows_Server_2019_V_253467_20250115_103045.ps1
│   └── Active_Directory_V_243467_20250115_104322.ps1
└── stig_library/              # STIG ZIP files (optional)
    ├── U_MS_Windows_Server_2019_V3R2_STIG.zip
    └── U_Active_Directory_Domain_V3R6_STIG.zip



🔧 Troubleshooting
AI Connection Issues

# Test AI connection
python estig_tool_ai.py -a
# Follow prompts to verify configuration

# Common issues:
# - Wrong base URL (check AI server address)
# - Model not loaded (ensure model is downloaded)
# - Firewall blocking connection
# - AI server not running

STIG Library Issues
No ZIP files found: Ensure STIG ZIP files are in the specified directory
No rules extracted: Verify ZIP files contain valid XCCDF XML files
Parsing errors: Check that ZIP files are not corrupted



Performance Tips
Increase timeout for complex STIG rules (200+ seconds)
Use faster models for quicker generation (smaller parameter models)
Close other applications to free up system resources during generation
🤝 Supported STIG Types
The tool supports all DISA STIGs that use the XCCDF format, including:

Operating Systems: Windows 10/11, Windows Server 2016/2019/2022, RHEL, Ubuntu
Applications: Microsoft Office, Adobe Products, Web Browsers
Services: Active Directory, DNS, IIS, SQL Server
Network Devices: Cisco routers and switches
Security Tools: Microsoft Defender, Trellix ENS
📝 Contributing
To extend or modify the tool:

Add new AI providers: Extend the generate_powershell_code() function
Support new formats: Modify the XCCDF parsing functions
Add validation types: Enhance the AI prompt templates
Improve error handling: Add more specific error cases
⚖️ License
This tool is provided as-is for STIG compliance management. Ensure compliance with your organization's policies when using AI-generated code.

🔗 Resources
DISA STIG Library
Ollama Documentation
LM Studio
STIG Viewer
Note: Always review AI-generated PowerShell code before use in production environments. The tool is designed to assist with STIG compliance but does not replace security expertise and validation.
