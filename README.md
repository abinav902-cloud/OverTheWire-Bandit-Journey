## 👨‍💻 About Me & My Goals
Hi! I am currently a +2 CBSE student balancing my passion for cybersecurity with my academic and personal goals. 

* 🎓 **Academics:** I am actively preparing for my Board Exams as well as the KEEM and JEE entrance exams. My ultimate goal is to secure a spot in a top engineering college in Kerala next year!
* 💻 **Cybersecurity:** I am dedicating time every day to build a strong foundation in Linux and ethical hacking, starting with this daily OverTheWire wargame journey. 
* 🏋️‍♂️ **Discipline & Health:** I strongly believe that a healthy body builds a sharp mind. I prioritize my health and hit the gym regularly, applying the exact same consistency and discipline to my fitness as I do to my studies and coding.

This repository is a daily log of my progress, proving that with consistency, you can balance academics, health, and learning new tech skills!
🛠️ Walkthrough & Methods (Levels 0 - 10)
Bandit Level 0 → Level 1
Goal: Log into the game using SSH.
Key Takeaways: Learned how to log into a remote server using the Secure Shell (SSH) protocol from a command-line terminal
.
Command: ssh bandit0@bandit.labs.overthewire.org -p 2220
Bandit Level 1 → Level 2
Goal: Read a file named - located in the home directory.
Key Takeaways: Learned how to read files with special characters that confuse standard commands
.
Command: cat ./-
Bandit Level 2 → Level 3
Goal: Read a file with spaces in its name.
Key Takeaways: Learned how to handle spaces in filenames by enclosing the file name in quotes or using escape characters
.
Command: cat "spaces in this filename"
Bandit Level 3 → Level 4
Goal: Find a hidden file in the inhere directory.
Key Takeaways: Learned that files starting with a dot (.) are hidden in Linux and require the -a (all) flag to be visible
.
Command: ls -a then cat .hidden
Bandit Level 4 → Level 5
Goal: Find the only human-readable file in a directory.
Key Takeaways: Learned how to discover the exact data type of a file using the file command to avoid printing binary gibberish to the screen
.
Command: file ./-file07
Bandit Level 5 → Level 6
Goal: Find a file hidden among dozens of directories based on specific properties.
Key Takeaways: Discovered the power of the find command to locate files based on exact byte size, readability, and executable status
.
Bandit Level 6 → Level 7
Goal: Find a file stored somewhere on the server owned by user bandit7 and group bandit6.
Key Takeaways: Learned how to search the entire root directory (/) and filter out "Permission denied" error messages by redirecting them to the trash (2>/dev/null)
.
Command: find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
Bandit Level 7 → Level 8
Goal: Find the password hidden next to the word "millionth" in a massive text file.
Key Takeaways: Learned how to instantly search for a specific word or pattern within a file using the Global Regular Expression Print (grep) command
.
Command: grep "millionth" data.txt
Password Captured: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
Bandit Level 8 → Level 9
Goal: Find the only non-repeating line of text in a file filled with duplicate garbage data.
Key Takeaways: Mastered piping (|)! Learned how to chain commands together by passing the output of cat into sort, and then strictly filtering out any duplicates using uniq -u
.
Command: cat data.txt | sort | uniq -u
Password Captured: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
Bandit Level 9 → Level 10
Goal: Extract a password hidden inside a binary data file preceded by several = characters.
Key Takeaways: Learned how to bypass unreadable binary gibberish by using the strings command to extract only human-readable text, then piping it directly into grep to pinpoint the flag
.
Command: strings data.txt | grep "==="
Password Captured: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
**Bandit Level 10 → Level 11**
*   **Goal:** Decode a password stored in `data.txt` which contains Base64 encoded data.
*   **Key Takeaways:** Learned the difference between raw data and encoded strings. Mastered using the `base64` utility with the `-d` (decode) flag to reveal hidden information.
*   **Command:** `base64 -d data.txt`
*   **Password Captured:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qR`
*   **Bandit Level 11 → Level 12**
*   **Goal:** Decrypt a password from `data.txt` using character rotation (ROT13).
*   **Key Takeaways:** Mastered the `tr` command for character-by-character translation. Learned how to create custom mapping rules to reverse simple substitution ciphers.
*   **Command:** `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
*   **Password Captured:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`
*   **Bandit Level 12 → Level 13**
*   **Goal:** Recover a password from a hexdump that has been repeatedly compressed.
*   **Difficulties Overcome:** Navigated a "Russian Nesting Doll" of file formats. Managed permissions by creating a workspace in `/tmp`.
*   **Key Takeaways:** 
    *   Mastered `xxd -r` to revert hexdumps to binary [5].
    *   Used `file` to identify nested compression layers [4].
    *   Chained `gzip -d`, `bzip2 -d`, and `tar -xf` for multi-stage extraction [5].
*   **Command Sequence:** 
    1. `xxd -r data.txt > data_binary`
    2. `file data_binary` (Iterative identification)
    3. `mv [file] [extension] && [tool] -d [file]` (Iterative extraction)
*   **Password Captured:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`
Bandit Level 13 → Level 14
Goal: Use the private SSH key found in the home directory (~/sshkey.private) to authenticate as user bandit14 and retrieve the password stored in /etc/bandit_pass/bandit14
.
Key Takeaways:
Identity-Based Authentication: Mastered the use of the ssh -i flag to log in using a cryptographic private key instead of a text password
.
Security Wall Bypass: Successfully navigated a server-side restriction that blocks internal localhost connections to port 2220 ("blocked to conserve resources") .
Credential Exfiltration: Learned to "pivot" by extracting the private key text and recreating it on a local workstation to connect as an external user .
Strict Permissions: Learned that SSH ignores private keys that are "too open." Using chmod 600 is mandatory to satisfy security protocols
.
Command: ssh -i bandit14.key bandit14@bandit.labs.overthewire.org -p 2220 
Password Captured: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS 
Bandit Level 14 → Level 15
Goal: Retrieve the password for Level 15 by submitting the current Level 14 password to a service listening on Port 30000 of localhost
.
Key Takeaways:
Network Interaction: Learned to use Netcat (nc) to establish direct TCP connections to specific network ports
.
Service Communication: Understood the concept of localhost as the current machine and how to "talk" to background services
.
Protocol Reliability: Used the TCP protocol for a reliable data transfer during the authentication handshake
.
Command: nc localhost 30000
Password Captured: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Bandit Level 15 → Level 16
Goal: Retrieve the Level 16 password by submitting the current password to a service listening on Port 30001 of localhost using SSL encryption
.
Key Takeaways:
Encrypted Handshakes: Mastered the use of openssl s_client to speak the "encrypted language" required by secure ports
.
Data Privacy: Learned that SSL/TLS provides certificates for server identification and encrypts traffic to prevent eavesdropping
.
Connection Management: Used the -ign_eof (Ignore End of File) flag to prevent the client from closing the connection before the server could reply
.
Command: openssl s_client -connect localhost:30001 -ign_eof
Password Captured: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Bandit Level 16 → Level 17
Goal: Identify the correct SSL service in a port range (31000-32000) and retrieve an RSA key for the next level
.
Key Tools & Commands:
Nmap (-A flag): Enabled aggressive service detection to identify which port was "speaking" SSL and which was the target service
.
chmod: Used chmod 600 to restrict permissions on the retrieved RSA key so it could be used for SSH
.
SSH Identity: Used the -i flag to authenticate using a private key file instead of a password
.
Methodology:
Scanned range: nmap -p 31000-32000 localhost
Interrogated target: nmap -A -p <port> localhost
.
Retrieved key via openssl s_client.
Saved key to a file and secured with chmod 600
.
Logged in: ssh -i bandit17.key bandit17@localhost -p 2220
.
Current Flag (Level 17): EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
