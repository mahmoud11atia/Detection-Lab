# Detection Engineering: Attack Simulation in Elastic SIEM

## Objective

This project built an isolated multi-VM lab to simulate attacker behavior and detect it in Elastic SIEM. I simulated a Meterpreter reverse shell, SYSTEM privilege escalation, and C2 exfiltration, then wrote 3 KQL detection rules from the telemetry the attacks generated, including a rule on PowerShell script block logging (Event ID 4104). All activity was performed in an isolated lab environment.

### Skills Learned

- Building and operating an isolated multi-VM lab (Windows, Ubuntu, Kali)
- Ingesting Windows Event Logs and PowerShell logging into Elastic SIEM
- Simulating attacker techniques and identifying the telemetry they leave behind
- Writing KQL detection rules and mapping them to MITRE ATT&CK
- Testing detections and documenting their logic and limitations

### Tools Used

- **Elastic Stack** (Elasticsearch, Kibana) for log ingestion, search, and detection rules
- **Metasploit / Meterpreter** for attack simulation
- **Kali Linux** as the attacker machine
- **Windows VM** as the victim, with PowerShell script block logging enabled
- **KQL** for detection logic

## MITRE ATT&CK Mapping

| Technique | ID | Simulated With | Detected By |
|-----------|----|----------------|-------------|
| PowerShell | T1059.001 | [Meterpreter / PowerShell payload] | [Rule 1 name] |
| Access Token Manipulation | T1134.001 | [getsystem / method you used] | [Rule 2 name] |
| Exfiltration Over C2 Channel | T1041 | [Meterpreter download / method you used] | [Rule 3 name] |

## Lab Architecture

[Insert diagram: VMs, network segment, Elastic server, log shipper/agent, attacker machine]

| Machine | OS | Role |
|---------|----|------|
| [Name] | Kali Linux | Attacker |
| [Name] | Windows [version] | Victim, log source |
| [Name] | Ubuntu | Elastic Stack server |

*Ref 1: Lab network diagram*

## Steps

### 1. Lab setup and log ingestion

[Describe how you deployed Elastic, installed the agent/Winlogbeat on the Windows VM, and confirmed logs were arriving.]

*Ref 2: Elastic receiving Windows logs in Kibana*

### 2. Enabling PowerShell script block logging

[Describe how you enabled logging, for example via Group Policy, and how you confirmed Event ID 4104 appeared in Elastic.]

*Ref 3: Event ID 4104 visible in Kibana Discover*

### 3. Attack simulation

**Reverse shell (T1059.001):** [What payload you used and how the session was established.]

*Ref 4: Meterpreter session opened from the Windows VM*

**Privilege escalation (T1134.001):** [How you escalated to SYSTEM.]

*Ref 5: Session running as NT AUTHORITY\SYSTEM*

**C2 exfiltration (T1041):** [What data you exfiltrated and over which channel.]

*Ref 6: Exfiltration activity from the attacker side*

### 4. Telemetry analysis

[Describe which events, fields, and Event IDs showed the attack in Elastic. This is what your rules are built on.]

*Ref 7: Attack telemetry in Kibana*

### 5. Detection rules

| # | Rule | ATT&CK | Log Source | Logic Summary |
|---|------|--------|------------|---------------|
| 1 | [PowerShell Script Block Detection] | T1059.001 | PowerShell Operational, Event ID 4104 | [What it looks for] |
| 2 | [Rule name] | [ID] | [Source] | [What it looks for] |
| 3 | [Rule name] | [ID] | [Source] | [What it looks for] |

```kql
// Rule 1: [name]
[paste your KQL query here]
```

Rule files: [`detection-rules/`](link)

*Ref 8: Detection rule configuration in Kibana*

### 6. Validation

[Re-ran each attack and confirmed the alert fired. Note anything that did not fire at first and what you changed.]

*Ref 9: Alert triggered in Kibana Security*

## Results

- [X] of 3 rules fired on the simulated attacks
- [Example: Script block logging exposed the payload content that process logs alone did not]

## Limitations and Next Steps

- **False positives:** [What legitimate activity could trigger each rule]
- **Evasion:** [How an attacker could bypass each rule, for example obfuscation]
- **Next steps:** convert the rules to Sigma, add more techniques (credential access, persistence), and tune thresholds.

## Disclaimer

All attack simulation was performed in an isolated lab environment on systems I own. No production or employer data was used.
