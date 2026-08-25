# Azure Cost Optimization Report

## Executive Summary
This report documents the identification, analysis, remediation, and prevention of unused Azure resources in the **Dev subscription**.  
The optimization pipeline was built using **Azure CLI, KQL Resource Graph, PowerShell, Bicep, Azure Policy, and Bing Copilot prompting**.  
Estimated savings: **$13.88/month ($166.56/year)**.

---

## Findings
- **2 unattached 32GB SSD disks** detected in `rg-dev-optimization`
- **1 unused Public IP address** detected in the same resource group
- Resources tagged with `env=dev` but not actively in use

---

## Savings Analysis
- **Azure Pricing Calculator (East US)** estimated monthly waste: $13.88  
- Annualized savings: $166.56  
- **Azure Advisor** confirmed recommendations for resource cleanup

---

## Remediation Actions
- **PowerShell script** executed with guardrails:
  - `env=dev` tag filter
  - 30‑day cutoff for unused resources
  - CSV export for audit trail
  - `-WhatIf` dry run + YES confirmation
  - Resource lock check
  - Transcript logging

---

## Prevention Measures
- **Azure Monitor Alert (Bicep)**: Daily detection of unattached disks  
- **Azure Policy (JSON)**: Deny creation of Public IPs without `env` tag  
- Governance guardrails ensure long‑term compliance and cost control

---

## Business Impact
- Reduced waste by **$166/year** in dev subscription  
- Automated detection + prevention ensures sustainable savings  
- Demonstrates **AI‑assisted cloud governance** using Bing Copilot + human validation

---

## Key Learnings
- Copilot is ~80% accurate for KQL and PowerShell, but **manual validation is mandatory**  
- Azure CLI `--query` syntax requires careful review; hallucinations observed in JMESPath  
- Combining **AI prompting + human oversight** accelerates optimization while maintaining reliability

---

## Next Steps
- Extend monitoring to **Prod subscriptions**  
- Add **cost anomaly detection** using Azure Cost Management APIs  
- Document remediation playbooks for broader IT support teams
