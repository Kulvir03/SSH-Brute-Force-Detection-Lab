# SSH-Brute-Force-Detection-Lab

This project demonstrates a simulated SSH brute-force attack from Kali Linux against a Windows machine with OpenSSH enabled. The attack is captured in Wireshark, and logs can be analyzed or sent to Splunk for detection testing.

---

## 🔧 What I Built

* Simulated an SSH brute-force attack using Hydra from a Kali Linux VM.
* Captured the attack using **Wireshark** on the victim machine.
* Attempted to detect the brute-force behavior using network traffic and log data.

---

## 🧰 Tools Used

* Kali Linux (Attacker)
* Hydra (Brute-force tool)
* rockyou.txt wordlist
* Wireshark (Packet capture)
* Windows 11 (Target with OpenSSH Server enabled)
* VMware Workstation (for virtualization)

---

## 📸 Key Steps

1. **Setup**:

   * Enabled OpenSSH Server on the Windows VM
   * Allowed port 22 through the firewall using PowerShell
   * Verified the SSH service with: `netstat -an | findstr ":22"`

2. **SSH Access Test**:

   * Verified SSH login manually: `ssh testy@<target-ip>`
   * Checked password prompt using both terminal and sshpass

3. **Brute Force Execution**:

   * Ran Hydra:

     ```bash
     hydra -l testy -P /usr/share/wordlists/rockyou.txt ssh://<target-ip>
     ```
   * Observed login attempts in terminal and monitored failures

4. **Wireshark Capture**:

   * Filtered traffic using: `tcp.port == 22`
   * Saved the packet capture as `.pcapng` for documentation

5. **Post-Attack Review**:

   * Observed thousands of SSHv2 packets
   * Detected repeated `RST, ACK` responses (connection resets)
   * Brute-force confirmed by packet count and encryption patterns

---

## 📊 Observations

* \~10,000 packets captured in under a minute
* Many encrypted packets and resets visible in Wireshark
* Wireshark showed SSH handshake attempts and repeated failures

---

## 💡 What I Learned

* How to simulate a brute-force SSH attack using Hydra
* How to enable and test OpenSSH Server on Windows
* Capturing and analyzing network traffic with Wireshark
* Recognizing signs of brute-force behavior from packet traces

---

## 📁 Files
[bfcapture.zip](https://github.com/user-attachments/files/20993173/bfcapture.zip) : Full Wireshark capture of the attack

* Screenshots of Hydra output and SSH login attempts


> **Note:** This lab was performed on an isolated virtual network and intended purely for educational and defensive purposes.
