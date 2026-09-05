# 📌 Project Summary
This project covers building a personal penetration-testing and cybersecurity lab using VirtualBox as the virtualization platform and Kali Linux as the security-focused operating system.
The goal is to build an enclosed, repeatable environment where tasks like scanning networks, gathering reconnaissance data, checking for vulnerabilities, and running other offensive-security exercises can happen without any risk to outside systems.
The environment runs on its own isolated virtual network, leaving room to plug in extra machines later that can serve as practice targets for sanctioned testing.

# 🎯 Goals
This project sets out to:
	•	Get VirtualBox installed and set up.
	•	Bring in a Kali Linux virtual machine (via install or import).
	•	Build a private NAT Network dedicated to the lab.
	•	Set up networking for the Kali VM.
	•	Give the Kali machine a fixed IP address.
	•	Confirm the network works and that DNS lookups succeed.
	•	Save a fresh snapshot of the VM as a restore point.
	•	Write up the whole build process.
	•	Get the environment ready for future security-related work.
# 🛡️ What the Lab Is For
This setup gives you a sealed-off space for practicing cybersecurity skills and running tests you’re authorized to perform.
Typical uses include:
	•	Mapping out networks
	•	Scanning for open ports
	•	Assessing vulnerabilities
	•	Analyzing network packets
	•	Testing web application security
	•	Practicing exploitation techniques
	•	Trying out new security tools
    
⚠️ Note: Only use this lab against machines you personally own or have clear authorization to test. Never point these tools at systems you don’t have permission to access.

# 🪜 Build Steps
# Step 1 — Get 7-Zip
7-Zip was needed to unpack the Kali Linux VM files, since they’re often packaged as a .7z archive.
Tool: 7-Zip
# Step 2 — Install VirtualBox
VirtualBox was set up to serve as the underlying hypervisor for the lab.
# Step 3 — Build the NAT Network
A separate NAT Network was configured inside VirtualBox with these settings:
	•	Network Name: NatNetwork
	•	IPv4 Range: 10.0.0.0/24
	•	DHCP: On
	•	IPv6: Off
<img width="4032" height="3024" alt="image" src="https://github.com/user-attachments/assets/d25f4699-6b70-47a2-88a7-85d629d62205" />

A NAT Network was chosen because it lets VMs on the same network talk to each other while still reaching the outside internet. This means attacker and target machines added later will be able to communicate with each other.
# Step 4 — Bring in Kali Linux
The Kali Linux VM image was pulled from Kali’s official site and loaded into VirtualBox.
Network adapter settings for the VM:
	•	Adapter 1
	•	Attached to: NAT Network
	•	Network: NatNetwork
	•	Adapter Type: Intel PRO/1000 MT Desktop
Memory allocated to the VM: 2048 MB
<img width="4032" height="3024" alt="image" src="https://github.com/user-attachments/assets/29fc0a42-1ac1-48f5-a56f-9e9f1afee5db" />

A shared folder was also set up to move files back and forth between the host machine and the Kali VM.
# Step 5 — Set Up Kali’s Network Settings
Kali’s network configuration was reviewed and locked to a fixed IPv4 address:
	•	IP: 10.0.0.2	
	•	Gateway: 10.0.0.1
Keeping the IP address fixed makes documentation and future exercises easier since the Kali machine’s address won’t change.
<img width="4032" height="3024" alt="image" src="https://github.com/user-attachments/assets/3fb1c137-1ba6-40d6-9d2e-d3bbf9331f6b" />

# Step 6 — Save a Baseline Snapshot
Once the initial setup was finished, a snapshot was taken in VirtualBox.
Example name: My Kali Linux setup:
This snapshot acts as the starting point for the lab — if a later exercise breaks or alters the configuration, the VM can be rolled back to this state.

# Issues Faced & Fixes
While downloading the 2026 release of the Kali VM, the import kept failing partway through — it aborted repeatedly and wouldn’t complete. Switching to the 2025 release solved the issue, and the import went through without any problems.

# 📚 What I Learned from this 
•	Taking a snapshot right after the initial setup turned out to be a good habit, since it gives a safe point to fall back to if a future exercise breaks the configuration.

•	Verifying each layer separately (interface config, gateway, internet access, DNS, and tool installation) made it much easier to pinpoint exactly where something was going wrong, rather than treating “the network” as one single thing to debug.

•	Troubleshooting a failed VM import is often about the source file or version rather than the VirtualBox configuration itself — before digging into settings, it’s worth testing whether a different build of the same OS resolves the problem.
