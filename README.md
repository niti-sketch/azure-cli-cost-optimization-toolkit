# Azure CLI Cost Optimization Toolkit with Bing Copilot

## Project Overview
An end-to-end Azure cost optimization pipeline built in a **single Bing Copilot chat thread** using guided prompting.  
The toolkit detects unused resources, validates savings, automates cleanup with guardrails, and prevents future waste using Azure CLI, KQL, PowerShell, Bicep, and Azure Policy.

---

## Problem Statement
Cloud environments often accumulate **orphaned resources** (unattached disks, unused IPs) that generate unnecessary costs.  
This project demonstrates how to identify, remediate, and prevent such waste in a **Dev subscription**.

---

## Solution Workflow (GESC Prompting)
1. **Discovery**  
   - Found 2 unattached 32GB SSD disks + 1 unused Public IP in `rg-dev-optimization`  
   - Tools: Azure CLI + KQL Resource Graph  

2. **Analysis**  
   - Validated waste at **$13.88/month ($166.56/year)**  
   - Tools: Azure Pricing Calculator (East US) + Azure Advisor recommendations  

3. **Remediation**  
   - PowerShell script with safety guardrails:  
     - `env=dev` tag filter  
     - 30-day cutoff  
     - CSV export  
     - `-WhatIf` + YES confirmation  
     - Resource lock check  
     - Transcript logging  

4. **Prevention**  
   - Bicep-based Azure Monitor alert for daily detection  
   - Azure Policy JSON to deny Public IP creation without `env` tag  

---

## Tech Stack
- **Azure CLI**  
- **KQL Resource Graph**  
- **PowerShell**  
- **Azure Advisor**  
- **Azure Pricing Calculator**  
- **Bicep**  
- **Azure Policy**  
- **Bing Copilot (prompt engineering)**  

---

## Repository Structure

/scripts/cleanup-disks.ps1  
PowerShell script to safely delete unattached disks with guardrails (tag filter, cutoff date, CSV export, -WhatIf dry run, YES confirmation, resource lock check).

/policies/deny-public-ip.json  
Azure Policy JSON to enforce governance by denying creation of Public IPs without the required `env` tag.

/alerts/unattached-disks.bicep  
Bicep template to deploy an Azure Monitor alert that triggers daily if unattached disks > 0 in the subscription.

/docs/cost-optimization-report.md  
Markdown report template summarizing findings, savings, risks, and prevention strategy for cost optimization.


---

## Key Learnings
- Copilot is ~80% accurate for KQL and PowerShell, but **manual validation is mandatory**.  
- Azure CLI `--query` syntax requires careful review; Copilot hallucinated Bicep functions in JMESPath.  
- Combining **AI prompting + human validation** accelerates cloud optimization but governance guardrails are essential.  

---

## Business Impact
- Reduced waste by **$166/year** in dev subscription.  
- Automated detection + prevention ensures long-term savings.  
- Demonstrates **AI-assisted cloud governance** for enterprise environments.  

---
