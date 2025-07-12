# Phishing Attack Simulation with Reverse Shell

This project simulates a real-world phishing attack where a fake login page is used to steal credentials, and a malicious EXE file is used to establish a reverse shell to the attacker's machine. The full attack is captured and analyzed using Wireshark.

---

##  Scenario

- Attacker: Kali Linux VM
- Victim: Windows 10 VM
- Objective: Steal credentials and gain remote shell access
- Tools Used: SET Toolkit, Metasploit, Wireshark

---

## Steps Performed

### 1. Generated Fake Login Page and Payload
- Used **Social Engineering Toolkit (SET)** to clone Google's login page
- Created a `fake_update.exe` payload using `msfvenom`

### 2. Launched Apache Web Server
- Hosted the payload on port 8080
- Victim downloaded it via phishing link

### 3. Captured User Credentials
- User submitted email and password to fake page
- Captured using SET logs and verified in Wireshark

### 4. Executed Reverse Shell
- User ran `fake_update.exe`
- Kali listener received a Meterpreter shell
- Session established and then closed

---

## Wireshark Packet Analysis

The attack was captured using Wireshark and saved as `.pcap`:

| Attack Stage        | Packet Filter Used | Description |
|---------------------|--------------------|-------------|
| EXE Download        | `http.request.uri contains "fake_update.exe"` | Shows GET request from victim |
| Credential Theft    | `http.request.method == "POST"` | Captured POST login details |
| Reverse Shell       | `tcp.port == 4444` | Meterpreter reverse TCP connection |

---

##  Screenshots

| Description                              | File Name                                 |
|------------------------------------------|--------------------------------------------|
| Malicious EXE Download                   | `malware_reverse_shell.png`                |
| Meterpreter Session Start & Close        | `meterpreter_session_started_and_closed.png` |
| Credentials Captured in POST             | `passwords_exposed.png`                    |
| Reverse Shell Traffic in Wireshark       | `reverse_shell_attack_captured.png`        |
| SET Logs Showing Email and Password      | `password_captured_after_fake_login_site.png` |

See the `/screenshots` folder for full images.

---

## Detection & Prevention Tips

| Threat                      | Defense Strategy                                  |
|----------------------------|---------------------------------------------------|
| Credential Harvesting      | Use MFA, email security, DNS filtering            |
| Malicious EXE Execution    | Use application allowlists, antivirus             |
| Reverse Shell Connections  | Monitor outbound ports, use SIEM, enable EDR      |

---

## 📁 Files Included

- `wireshark.pcapng`: Full network capture of attack
- `screenshots/`: Evidence and documentation of each stage

---

##  What I Learned

- How phishing attacks steal credentials using fake websites
- How malicious payloads can open remote shells
- How to use Wireshark to detect reverse shell behavior
- How to document cyber attacks for investigation

---



##  Author

- GitHub: [tinayeisher0](https://[github.com/tinayeisher0]
- Project Date: July 2025
