# Scanning and Internal Reconnaissance

Now that we are inside the network of our target, we will now perform reconnaissance inside the internal network, known as **active reconnaissance**, in order to reveal which devices are on the network and what potential new targets await.

- We call this **active reconnaissance** because we are now directly interacting with our target.
- It is also considered **internal reconnaissance** because we are conducting this *internally* within the target. 
- While inside the network, we can gather the following:
    - Information about the host, known as **host enumeration**.
    - Information about processes on the system, known as **process enumeration**.
    - Information about the users on the system.


# Scanning

Additionally, we can more aggressively gather information through a process called **scanning**.

  - **Scanning** is the second phase of a pen testing engagement, after Planning and Reconnaissance. Scanning uses tools to gather information such as network information and potential vulnerabilities.
    - While in our example we scanned our target from inside the network, scanning is often conducted externally, before initial access.
  - **Nessus**, **Hping**, and **Nmap** are tools which we often utilize to conduct scanning.
  - **Zenmap** is the GUI version of Nmap. It provides an easy-to-use tool to automate scanning tasks.
  - **NSEs (Nmap scripting engines)** are scripts that are commonly used to test whether a service is vulnerable to an exploit. 
  - **SearchSploit** is a command-line utility for Exploit-DB that allows you to take an offline copy of the Exploit Database with you wherever you go.
