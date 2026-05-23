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
