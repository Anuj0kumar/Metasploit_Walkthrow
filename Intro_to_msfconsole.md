## What is msfconsole?

Think of **msfconsole** as your control panel for the Metasploit Framework.
It’s the most popular interface that allows you to interact with all of Metasploit’s powerful features, including exploits, payloads, and post-exploitation modules.
It even lets you run external commands, making it a versatile tool for penetration testers.


---

### Getting Started: Setting Up Your Environment

Before you launch `msfconsole`, you need to ensure Metasploit's database is running.
This database is essential for storing your penetration testing results and managing your sessions.

* **To start it, simply use:**
    ```
    service postgresql start
    
    ```

* **Launch msfconsole:**
    Once the service is active, you can launch it by typing:
    ```
    msfconsole
    
    ```
    <img width="1200" height="819" alt="image" src="https://github.com/user-attachments/assets/7cbd2794-3ec3-44f4-ac6b-8f7f634c8081" />


* **Quiet Mode:**
    You can also start it in "quiet mode" to skip the initial banner by using `msfconsole -q` .

---

### Essential msfconsole Commands for Beginners

Here are several fundamental commands that are helping us while working with Metasploit:

* **help:** to understand the working of commands. Type `help` to get a list of all available commands and their descriptions.
* **show:** This command is incredibly useful for exploring Metasploit’s vast library. We can use it to:
    * `show exploits`  to list all available exploits.
      <img width="1918" height="546" alt="image" src="https://github.com/user-attachments/assets/14d79f62-539b-4d57-aa1a-30e4cd1c3852" />

    * `show payloads`  to see the different payloads you can use.
      <img width="1710" height="524" alt="image" src="https://github.com/user-attachments/assets/5de81b24-94a9-48de-9de2-30218a3ea951" />

    * `show auxiliary` to list auxiliary modules for scanning and reconnaissance.
      <img width="1918" height="470" alt="image" src="https://github.com/user-attachments/assets/68c0480a-4cb4-4d70-a891-cc21898396f9" />

* **use:** Once you've found an exploit or module you want to use, the `use` command loads it into your current session.
    * *Example:* `use exploit/windows/smb/ms17_010_eternalblue` .
* **show options:** After loading a module, `show options` is critical. It displays all the configurable parameters you need to set before running the exploit, such as **RHOST** (remote host/target IP) and **RPORT** (remote port).

  <img width="1903" height="804" alt="image" src="https://github.com/user-attachments/assets/7fb3553d-8f2d-4951-b8b1-03c4b53d3d7f" />
* **set:** This command allows you to configure the options displayed by `show options` .
    * *Example:* `set RHOST 192.168.1.105` to specify your target.
* **info:** Get detailed information about a loaded module, including its description, platform compatibility, and references.
  <img width="1302" height="544" alt="image" src="https://github.com/user-attachments/assets/f0b1e3ad-62d9-4c12-b86c-3d9970c3b8e8" />

* **back:** If you need to exit a loaded module and return to the main `msfconsole` prompt, simply type `back`.

---

### Live Demo of Eploitation: From Scan to Shell!

The demonstration of exploiting a Metasploitable machine from Kali Linux :

1.  **Scan the target** using `nmap` to identify open ports and services. This is crucial for understanding the target's vulnerabilities.
   <img width="1158" height="686" alt="image" src="https://github.com/user-attachments/assets/959d56cd-11d8-414f-a601-cca92f441cd0" /><br>

3.  **Search for relevant exploits** based on the identified services.
   <img width="1444" height="380" alt="image" src="https://github.com/user-attachments/assets/184e16fc-7e11-4c2e-993b-ecdef7d6ba62" /><br>


5.  **Load the chosen exploit** using the `use` command.
  <img width="1429" height="622" alt="image" src="https://github.com/user-attachments/assets/112c84e7-1f29-49d3-b541-cf42e3579cde" /><br>

7.  **Set the necessary options**, particularly the `RHOST` (target IP address).
8.  **Execute the exploit** using the `exploit` command.
<img width="1920" height="982" alt="Screenshot_2026-01-13_06_26_40" src="https://github.com/user-attachments/assets/d43c3ba9-85db-4faf-9909-ab7a476e409f" />

> **The result?** A successful command shell on the target machine, demonstrating the power of Metasploit in action!

---

### Managing Sessions

After gaining access, Metasploit allows you to manage multiple sessions.

* **Background a session:** Use `Ctrl+Z` and then `y` to continue working within `msfconsole`.
* **List active sessions:** Use `sessions -l`.
* **Interact with a session:** Use `sessions -i <ID>`.
