Cracking Hashes with Hashcat: A Step-by-Step Guide

This guide details the process of cracking two different hashes using Hashcat on a Linux environment, leveraging a wordlist for dictionary attacks.

1. Environment Setup: Installing Hashcat
First, ensure your Linux system is up to date and then install Hashcat.

Update Package Manager:
To begin, I updated my system's package manager to ensure all existing packages were current and to fetch the latest information on available software.

Bash

sudo apt update
This command refreshes the package lists from the repositories.

Install Hashcat:
Next, I installed Hashcat, a powerful open-source password recovery tool.

Bash

sudo apt install hashcat
As shown in 1-install hashcat.jpg, Hashcat was already the newest version (6.2.6+ds2-1bl), so no installation was actually performed, but the system confirmed its presence.

2. Preparing the Wordlist: rockyou.txt
Before attempting to crack any hashes, a wordlist is essential for dictionary attacks. Hashcat will hash each word in this list and compare it to the target hash.

Download rockyou.txt:
I navigated to the ~/Documents/Masterschool directory, as seen in 5-ubication.png. In Kali Linux, rockyou.txt is typically pre-installed, so I confirmed its presence in this directory.

Bash

cd ~/Documents/Masterschool
ls
# Expected output should show rockyou.txt
3. Cracking Hash 1: fde24d80ac225175b4be937fdb1fab97
Identify Hash Type:
The first step was to identify the type of Hash 1. I used the online "Hash Analyzer" tool from TunnelsUP.com (3-hash1 type.jpg).

Input Hash: fde24d80ac225175b4be937fdb1fab97

Result: The tool identified it as MD5 or MD4. Hashcat uses specific mode numbers for different hash types. For MD5, the mode is 0.

Create Hash File:
To provide Hashcat with the target hash, I created a file named HASH1 and saved the hash within it.

Bash

touch HASH1
nano HASH1
Inside nano, I pasted fde24d80ac225175b4be937fdb1fab97. After pasting, I pressed CTRL + X, then Y to save, and Enter to confirm the filename, as depicted in 2-hash1-nano.png.
To verify the content, I used cat:

Bash

cat HASH1
# Output: fde24d80ac225175b4be937fdb1fab97
Execute Hashcat Command:
Now, with the hash file and wordlist ready, I executed the Hashcat command to start the cracking process.

Bash

hashcat -m 0 -a 0 HASH1 rockyou.txt
-m 0: This flag specifies the hash type. 0 corresponds to MD5.

-a 0: This flag specifies the attack mode. 0 corresponds to a dictionary attack.

HASH1: This is the file containing the hash to be cracked.

rockyou.txt: This is the wordlist used for the dictionary attack.

The cracking process is shown in 4-crack hash1.jpg. Hashcat successfully cracked the hash, revealing the plain text password. The output indicated a "Cracked" status and showed the result.

4. Cracking Hash 2: 2d354a2fb4066717f86d5a5f633e14f8538018c3
Identify Hash Type:
Similar to Hash 1, I used the TunnelsUP.com Hash Analyzer (7-hash2 type.jpg) to identify the type of Hash 2.

Input Hash: 2d354a2fb4066717f86d5a5f633e14f8538018c3

Result: The tool identified it as SHA1 (or SHA 128). For SHA1, Hashcat mode 100 is used.

Create Hash File:
I created a new file named HASH2 to store the second hash.

Bash

touch HASH2
nano HASH2
Inside nano, I pasted 2d354a2fb4066717f86d5a5f633e14f8538018c3. I then saved and exited.
I verified the content:

Bash

cat HASH2
# Output: 2d354a2fb4066717f86d5a5f633e14f8538018c3
The ls command also confirms both hash files and the wordlist are in the directory (6-hash2-cat.png).

Execute Hashcat Command:
Finally, I executed Hashcat for the second hash.

Bash

hashcat -m 100 -a 0 HASH2 rockyou.txt
-m 100: This flag specifies the hash type as SHA1.

-a 0: This again indicates a dictionary attack.

HASH2: The file containing the second hash.

rockyou.txt: The wordlist used.

As shown in 8-crack hash2.jpg, Hashcat successfully cracked this hash as well, providing the plaintext password.# hashcat
Crack a Hash with Hashcat
