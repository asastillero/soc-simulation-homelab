# Home Lab SOC Simulation – Windows Endpoint + Wazuh SIEM

**Author:** Aino Astillero  
**Date:** July 23, 2025

## 🔍 Project Overview

This project simulates a real-world SOC analyst workflow using a home lab setup. The primary goal was to detect and analyze simulated malicious activity on a Windows endpoint using Wazuh SIEM.

## 🛠️ Environment

- **SIEM Server**: Ubuntu VM (VirtualBox) with Wazuh Manager
- **Monitored Host**: Windows 10 VM with:
  - Wazuh Agent
  - Sysmon (system activity monitor)
- **Communication**: Agent registered and connected to Wazuh Manager

## 💥 Simulated Attack (malware_sim.py)

A Python script was executed on the Windows endpoint to simulate common malware behaviors:

1. Wrote a malicious registry key (Run persistence)
2. Created a scheduled task to run `calc.exe` every 5 minutes
3. Launched suspicious processes: `cmd.exe`, `PowerShell`, `calc.exe`

## 📊 Detection and Alerts

The following MITRE ATT&CK techniques were triggered and detected:

| Technique ID | Technique Name                 | Tactic(s)                                |
|--------------|--------------------------------|-------------------------------------------|
| T1059.001    | PowerShell Execution           | Execution                                 |
| T1078        | Valid Account                  | Persistence, Privilege Escalation         |
| T1087        | Account Discovery              | Discovery                                 |
| T1105        | Remote File Copy (C2)          | Command and Control                       |
| T1547        | Registry Run Key / Startup     | Persistence                               |

✅ Wazuh successfully detected and alerted all activity with corresponding rule IDs (e.g., `92031`, `92201`, etc.)

## 📁 Artifacts

- `malware_sim.py` – the attack simulation script
- `screenshots/` – screenshots of alerts, persistent opening of calculator, log entries, incident response
- `logs/` – ossec.log
- `Home_Lab_SOC_Simulation_Report_Aino_Astillero.pdf` – full report

## 🧠 Lessons Learned

- SIEM detection and logging were effective with default Wazuh ruleset
- Sysmon significantly enhanced visibility
- Agent disconnections can happen due to IP changes, solved via agent re-registration. This is unlikely to happen in real world scenario as IP addressing would be in static format.

## 📝 Next Steps

➡️ Proceed to:
- Vulnerability Management Workflow (OpenVAS/Nessus + OWASP Juice Shop)
- Push this repo to GitHub for portfolio visibility

---

### 🔗 Usage

To simulate this yourself:

1. Clone this repo
2. Deploy Ubuntu and Windows VMs
3. Install Wazuh and Sysmon
4. Execute the script and monitor alerts on the Wazuh dashboard

---

