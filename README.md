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
Bandit Level 17 → Level 18
Goal: Find the password for Level 18, which is the only line that has been changed between passwords.old and passwords.new
.
Key Tools & Commands:
diff: Used to compare the two files and display the line-by-line differences
.
cat: Used (previously) to retrieve the physical password for Level 17 from /etc/bandit_pass/bandit17.
Methodology:
Identify the files: Confirmed the presence of passwords.old and passwords.new in the home directory.
Compare content: Ran diff passwords.old passwords.new .
Analyze output: The command identified the line removed from the first file (<) and the line added to the second file (>).
Extract Flag: The line marked with > in the second file was the new password.
Password for Level 18: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
Bandit Level 18 → Level 19
Goal: Retrieve the password for Level 19 from the readme file in the home directory of user bandit18.
The Challenge: The user account has a modified .bashrc file that prints "Byebye!" and terminates the SSH connection immediately upon login.
Key Tools & Concepts:
SSH Command Arguments: Passing a command as an argument to SSH to execute it on the remote host without starting an interactive shell.
Shell Initialization: Understanding that .bashrc only triggers for interactive login shells.
Methodology:
Direct Execution: Ran the command: ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme ].
Authentication: Provided the password for Level 18: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO .
Result: The server printed the contents of readme and closed the connection, bypassing the logout trap.
Password for Level 19: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8 .
Bandit Level 19 → Level 20
Goal: Retrieve the password for Level 20 stored in /etc/bandit_pass/bandit20.
The Challenge: User bandit19 lacks read access to the target file. The solution requires using a SetUID binary in the home directory .
Key Tools & Concepts:
SetUID Binary: A file with the Set User ID bit set (visible as s in ls -l), which runs with the owner's privileges.
bandit20-do: A "wrapper" binary owned by bandit20 that executes user-provided commands with elevated permissions.
Methodology:
Identify the Binary: Ran ls -l to locate ./bandit20-do and confirmed the s bit in its permissions .
Execute with Privilege: Used the binary to read the protected file: ./bandit20-do cat /etc/bandit_pass/bandit20.
Result: The command printed the password for Level 20 by leveraging the binary owner's access rights.
Password for Level 20: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO.
Bandit Level 20 → Level 21
Goal: Retrieve the password for Level 21 using the suconnect binary in the home directory.
The Challenge: The binary is a SetUID program that connects to a specified localhost port, reads the current level's password from that connection, and (if correct) transmits the next level's password back through the same connection.
Key Tools & Concepts:
Netcat (nc): Used to create a network listener that acts as a temporary server .
SetUID Binaries: Programs that run with the file owner's permissions (in this case, bandit21).
Multi-Terminal Interaction: Opening two simultaneous SSH sessions to perform a "handshake" .
Methodology:
Terminal A (The Listener): Started a Netcat listener on a random port (e.g., nc -l -p 1234) .
Terminal B (The Client): Ran the SetUID binary and instructed it to connect to the listener: ./suconnect 1234 .
The Handshake: In Terminal A, provided the Bandit 20 password. The binary in Terminal B received it, verified it, and printed the password for Level 21 .
Password for Level 21: EeoULMCra2q0dSkYj561DX7s1CpBuOBt.
Bandit Level 21 → Level 22
Goal: Retrieve the password for Level 22 by investigating an automated process
.
Key Tools & Concepts:
Cron: A time-based job scheduler in Unix-like systems
.
Directory Navigation: Investigated /etc/cron.d/ for system-wide task configurations
.
Shell Script Analysis: Read a .sh file to understand how it manipulated data and file permissions
.
Redirection (>): Identified how the script sent the password output to a temporary file
.
Methodology:
Used ls /etc/cron.d/ to find the scheduled task named cronjob_bandit22
.
Used cat /etc/cron.d/cronjob_bandit22 to find the path of the script being executed: /usr/bin/cronjob_bandit22.sh
.
Inspected the script with cat, revealing that it copied the Level 22 password to a specific file in /tmp/
.
Read the temporary file to retrieve the password
.
Password for Level 22: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q .
Bandit Level 22 → Level 23
Goal: Retrieve the password for Level 23 by reverse-engineering a dynamic automated process.
Key Tools & Concepts:
Cron: Utilized as a background scheduler to run scripts at 1-minute intervals
.
MD5sum: Used to generate a unique hash based on a specific string ("I am user bandit23")
.
Logic Emulation: Manually running script variables to identify hidden output locations.
Methodology:
Located the cron configuration in /etc/cron.d/cronjob_bandit23
.
Inspected the executable script: /usr/bin/cronjob_bandit23.sh
.
Analyzed the logic: The script identified its target filename by hashing the string "I am user $myname" .
Executed the command manually to find the hash: echo I am user bandit23 | md5sum | cut -d ' ' -f 1 .
Read the resulting file in /tmp/8ca319486bfbbc3663ea0fbe81326349 to retrieve the password .
Password for Level 23: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga.
Bandit Level 23 → Level 24
Goal: Retrieve the password for Level 24 by creating a shell script and hijacking an automated cron job
.
Key Tools & Concepts:
Shell Scripting: Authored a .sh file with a bash shebang
.
Cron Jobs: Exploited a task-scheduler running as a higher-privileged user
.
File Permissions: Used chmod 777 to allow a multi-user write environment
.
Output Redirection: Used > to save command output to a specific file
.
Methodology:
Analyzed the cron job configuration in /etc/cron.d/cronjob_bandit24.
Inspected the execution script at /usr/bin/cronjob_bandit24.sh and found it executes and deletes files in /var/spool/bandit24/foo/ .
Created a workspace in /tmp/abi and granted full permissions.
Wrote solve.sh to execute cat /etc/bandit_pass/bandit24 > /tmp/abi/password.txt .
Copied the script to the spool folder and waited for the 60-second execution cycle
.
Password for Level 24: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
Goal: Retrieve the password for Level 25 by brute-forcing a numeric 4-digit PIN against a network daemon listening on port 30002
.
Key Tools & Concepts:

    Bash Scripting: Utilized a for loop to automate 10,000 combination attempts

.
Networking with Netcat: Used nc to establish a TCP connection to the service on port 30002
.
Piping: Employed the | operator to redirect the loop's generated output directly as input to the network command
.
Sequential Expansion: Leveraged the {0000..9999} syntax to handle 4-digit padding with leading zeros automatically

    .

Methodology:

    Connected to the daemon on localhost 30002 using nc and confirmed it required the bandit24 password followed by a space and a PIN on a single line

.
Determined that manual entry was unfeasible for the 10,000 combinations (0000-9999)
.
Constructed a Bash one-liner script to generate the required input stream: for i in {0000..9999}; do echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"; done
.
Piped the results of the loop into the nc command: | nc localhost 30002
.
Monitored the output stream for the unique "Correct!" message containing the next level's credentials

    .

Password for Level 25: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
Bandit Level 25 → Level 26 Walkthrough
Goal
Log in as bandit26 and break out of the restricted shell to retrieve the password for Level 27
.
Key Takeaways

    Shell Investigation: Users aren't always assigned /bin/bash. Some are assigned scripts that restrict their environment

.
Pager Interaction: The more command is interactive and can be used to launch external editors
.
Living off the Land: Using pre-installed tools (like Vim) to perform actions the administrator did not intend

    .

Technical Steps

    Identify the Shell: Run getent passwd bandit26 from Level 25. The output shows /usr/bin/showtext as the login shell

.
The Connection: Used the RSA key found in the home directory: ssh -i bandit26.sshkey bandit26@localhost -p 2220
.
The Breakout:

    Resize window: Shrink terminal to ~2 lines high.
    Trigger Pager: Run the SSH command; the more prompt appears.
    Escape to Vim: Press v.
    Spawn Bash:

Retrieve Password: cat /etc/bandit_pass/bandit26


Password for Level 26:s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
