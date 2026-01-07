🛡️ SOC Lab: Windows Endpoint Telemetry & SIEM Integration
📋 Project Overview
This project documents the deployment of a centralized Security Operations Center (SOC) monitoring solution using Wazuh (SIEM/XDR). The laboratory environment focuses on establishing a high-fidelity telemetry pipeline from a Windows 10/11 endpoint, integrating Sysmon for deep behavioral analysis, and resolving real-world enterprise networking challenges.

🏗️ Architecture & Stack
SIEM Manager: Wazuh Manager 4.x (Ubuntu Server)

Endpoint: Windows 10 (Agent Name: MOSES)

Log Shipper: Wazuh Agent (Configured for TCP/1514)

Telemetry Source: Microsoft Sysmon (SwiftOnSecurity configuration)

Network Mode: Bridged Adapter

🛠️ Engineering & Troubleshooting Log
One of the key outcomes of this project was the resolution of critical communication barriers between the endpoint and the manager.

1. Agent Authentication Collision
Issue: Encountered ERROR: Duplicate agent name: MOSES during registration.

Root Cause: A stale agent ID existed on the Manager from a previous installation attempt.

Resolution: Utilized the manage_agents -r utility on the Ubuntu Manager node to clear the legacy record, allowing a fresh authentication handshake.

2. Protocol Pivot: UDP to TCP
Issue: Agent status reported "Active" (Heartbeat OK), but zero event telemetry reached the dashboard.

Discovery: Used tcpdump on the Manager to verify that UDP/1514 packets were being silently dropped by the virtual network bridge.

Resolution: Migrated the log-shipping protocol in ossec.conf from UDP to TCP/1514. This established a stateful connection that bypassed packet-loss issues inherent in the bridged environment.

🔍 Telemetry & Detection Validation
To verify the pipeline, I monitored the raw archives.json on the Manager to confirm successful ingestion of Windows Event Channel data.

Captured Raw Event Proof
The following JSON snippet demonstrates the successful capture of Event ID 4798 (Local group membership enumeration), proving that the decoder is correctly parsing Windows XML into JSON:

JSON

{
  "timestamp": "2026-01-07T19:31:51.494+0000",
  "agent": {"id": "005", "name": "MOSES", "ip": "192.168.x.xxx"},
  "data": {
    "win": {
      "system": {
        "eventID": "4798",
        "message": "A user's local group membership was enumerated."
      }
    }
  },
  "location": "EventChannel"
}
High-Severity Alert Simulation
To validate the Alerting Engine, I simulated an anti-forensics technique:

Action: Executed wevtutil cl System (Clearing Windows System Logs).

Detection: Wazuh triggered a Level 10 (High Severity) alert (Rule ID: 510).

Result: Confirmed real-time visibility in the Wazuh Threat Hunting dashboard.

📂 Configuration Files
ossec.conf - Sanitized Wazuh Agent configuration.

sysmon-config.xml - Sysmon policy for behavioral tracking.

🚀 Future Roadmap
[ ] Implement Active Response to automatically block malicious IPs.

[ ] Integrate VirusTotal API for automated file integrity scanning.

[ ] Build a custom Dashboard for Sysmon Process Creation tracking.
