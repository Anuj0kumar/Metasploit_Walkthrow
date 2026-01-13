# Metasploit Payloads: Architecture and Classification

In the context of the Metasploit Framework, the terms **Exploit** and **Payload** represent distinct but complementary components of a penetration test.

Technically, the **Exploit** functions as the delivery mechanism designed to breach system defenses (such as firewalls or software vulnerabilities). The **Payload** is the operational code executed on the target system subsequent to a successful breach.

The payload dictates the post-exploitation capabilities available to the tester. These modules are classified according to three primary technical criteria: delivery method, operational capability, and connection direction.

<br><vr>

## Delivery Method: Inline vs. Staged

This classification refers to the structural composition of the payload and the method by which it is loaded into the target's memory.



###  Inline Payloads (Single)
Inline payloads are self-contained executable packages. They integrate the exploit and the shellcode into a single transmission unit.

* **Naming Convention:** Identified by an underscore (`_`).
* **Example:** `windows/shell_reverse_tcp`
* **Operational Context:** These are optimal for environments where stability is paramount, or in air-gapped scenarios where the target system lacks network access to retrieve additional data.

###  Staged Payloads
Staged payloads utilize a multi-step architecture.<br>
> Initially, a compact code stub known as the "Stager" is transmitted to establish a network connection.<br>
  Upon connection, the Stager retrieves the larger "Stage" component from the attacker's machine.

* **Naming Convention:** Identified by a forward slash (`/`).
* **Example:** `windows/shell/reverse_tcp`
* **Operational Context:** This is the standard method for modern exploitation. It circumvents memory space restrictions inherent in many vulnerabilities, allowing for the deployment of complex tools like Meterpreter.

<br><br>

## Operational Capabilities: Shell vs. Meterpreter

This category distinguishes the payload based on the interface and functionality provided to the operator.

| Payload Type | Technical Description | Primary Application |
| :--- | :--- | :--- |
| **Command Shell** | Provides a standard command-line interface (CLI) native to the target OS, such as `cmd.exe` on Windows or `/bin/sh` on Linux. | Utilized for lightweight, low-bandwidth connections or the execution of native system commands. |
| **Meterpreter** | An advanced, extensible payload that operates entirely via in-memory DLL injection. It avoids writing to the host disk, thereby minimizing forensic footprints. | The preferred tool for post-exploitation. It facilitates complex tasks such as privilege escalation, password hash dumping, and lateral movement. |

<br><br>

## Connection Direction: Bind vs. Reverse

This distinction defines the initiation of the network connection (handshake), a critical factor in bypassing network firewalls.



### Reverse Payloads (Connect-Back)
In this configuration, the target system initiates the connection back to the attacker’s listener.

* **Naming:** `reverse_tcp`, `reverse_http`, `reverse_https`
* **Used for:** This is the standard configuration for penetrating corporate networks. As most firewalls block unsolicited incoming traffic but permit outgoing traffic (e.g., HTTP/HTTPS), a reverse payload effectively mimics legitimate outbound communication.

###  Bind Payloads
In this configuration, the payload opens a listening port on the target system, awaiting a connection from the attacker.

* **Naming:** `bind_tcp`
* **Used for :** This method is employed when the target system is restricted from initiating outbound connections (e.g., due to strict egress filtering) but is accessible to the attacker. It is frequently used during lateral movement within an already compromised network.

<br><br>

## Some Common Payload Examples

The following examples illustrate the naming schema used within the Metasploit Framework:

* `windows/meterpreter/reverse_tcp`
    **Standard Windows Staged Payload:** Delivers the Meterpreter agent via a staged architecture, utilizing a reverse TCP connection to bypass ingress filtering.

* `linux/x64/shell_bind_tcp`
    **Linux Inline Payload:** A single-stage payload for 64-bit Linux architectures that opens a local port and provides a standard command shell upon connection.

* `java/meterpreter/reverse_http`
    **Cross-Platform Java Payload:** A staged Meterpreter payload that tunnels traffic over the HTTP protocol, often used to evade deep packet inspection (DPI) mechanisms.
