# SearchSploit 

Basically we can use a tool to determine which exploits we can attempt with the information that we gathered on our scans: Exploit-DB.

## Exploit-DB

The webpage **Exploit Database (Exploit-DB)**, at https://www.exploit-db.com/, is a popular online database that contains publicly disclosed exploits.  

- Penetration testers can search through this webpage to find exploits.
- The exploits are cataloged according to their **Common Vulnerability and Exposure (CVE)** identifiers.

- For example, Oracle Global Desktop 4.61.915 is an exploit listed on the Exploit-DB website.

 ![image](https://user-images.githubusercontent.com/118358126/203057445-89c21a78-98d1-47ec-b4cc-cb7d81f5d392.png)

- Notice that the CVE number assigned to this particular vulnerability is 2014-6278.

- CVE numbers typically start with the year in which the vulnerability was discovered (in this case 2014).

Exploit-DB's catalog of exploits is constantly updated as software developers patch their systems.

- Exploit-DB is run by Offensive Security, who also maintain Kali Linux and administrate several certifications, such as the OSCP.

## SearchSploit 

While the Exploit-DB website can be very useful, pentesters may conduct penetration tests from networks without internet activity, which makes it difficult to access the Exploit-DB website.

- This issue is addressed with a tool called **SearchSploit**.

**SearchSploit** is a command-line utility for Exploit-DB that allows you to take an offline copy of the Exploit Database with you wherever you go.

- SearchSploit allows security professionals to perform detailed offline searches of hundreds of exploit scripts through their local copy of the repository.
   
   - This capability is useful if you are working on a security assessment with an air-gapped, segregated network that lacks internet connectivity.
   
   - If you anticipate that you will not have internet connectivity during an assessment, update your local repo by checking out and downloading the most recent Exploit-DB repository while you still have access to the internet.

SearchSploit, as indicated by its name, will search for all exploits and shell code contained within the Exploit-DB repository.

 - SearchSploit comes preinstalled on Kali Linux, but should be updated on a weekly basis and prior to each use. 

### SearchSploit Showcase

This demo will detail how to use this VM to run a Shellshock exploit on the Shellshock VM, which is an intentionally vulnerable machine designed to test the Shellshock exploits.

In this demonstration, you will conduct the following steps:

- Run through some basic help commands that are useful when searching for exploit scripts. 
- Discuss the various file formats associated with SearchSploit exploit scripts.
- Break down the command syntax for the typical `searchsploit` command.
  
1. Begin by showing the SearchSploit help option. The `-h` flag provides information about proper command syntax, flags, and options.


2. As the name suggests, SearchSploit is a search tool. Let's perform a basic search:
  
    - Run `searchsploit ftp remote file`

    - This command will search the exploit database for the three terms: "ftp," "remote," and "file."

    - **Note**: SearchSploit uses an **and** operator by default.

![image](https://user-images.githubusercontent.com/118358126/203063764-f13257bf-bd3d-4416-8308-de158b5544dd.png)

3. By default, SearchSploit includes the title and path of the exploit in its query. Searches can be restricted to specific titles with the `-t` option. 

    - Run `searchsploit -t oracle windows`

![image](https://user-images.githubusercontent.com/118358126/203063865-aa9e2cea-1c9a-40e0-949f-8953cc8835d8.png)
   
   - The `wc -l` option will return the number of exploits in the search:     

   - `searchsploit -t oracle windows | wc -l`
   
   - Without the `-t` option, the command will search for results containing "oracle" **and/or** "Windows." 
   
       - `searchsploit oracle windows | wc -l`   
   
![image](https://user-images.githubusercontent.com/118358126/203064032-f53c8a72-cc92-4e61-8637-52835c663482.png)

4. We can leave out unwanted results with the `--exclude` option. We can remove multiple terms by separating the term values with a pipe `|`.

    - `searchsploit linux kernel 4.4 --exclude="(PoC)|/DCCP/"`

       - `--exclude="(PoC)|/DCCP/"`: Leaves out all lines that contain both "PoC" and "DCCP."

![image](https://user-images.githubusercontent.com/118358126/203064333-708e8d76-13b3-45ad-b326-ca61ad1ec88b.png)


5. To access more exploit metadata, such as setup files, vulnerability mappings, screenshots, and tags, we need to access the exploit-db.com website. The `-w` option will provide the website in the results. 

    - Run `searchsploit mysql 6.0 -w`

      The search query returns URLs for the webpages of the associated exploits.

![image](https://user-images.githubusercontent.com/118358126/203064500-952e3f8e-df89-4eae-b891-ebaa148bc65d.png)

   - Open the first link in a web browser and observe the results.

      - In the example below, we observe the results for **EDB-ID: 40465 (Exploit-DB ID #40465)**.

      - Exploit-DB provides expanded search results that contain more exploit details.

      - Scroll down the webpage for the full details of the exploit.
       
![image](https://user-images.githubusercontent.com/118358126/203065022-db7f0aca-ee42-4c9c-8a45-e9e6a7ede2e9.png)

6. SearchSploit exploit scripts come in a variety of file types, including `.rb`, `.py`, `.sh`, `.html`, and `.txt`.

    - `.rb`: Scripts written in Ruby, most likely for Metasploit, a penetration testing framework and C2 platform that we'll explore later
    - `.py`: Python
    - `.sh`: Bash
    - `.html`: HTML
    - `.txt`: text editor
   
    Run the following command: 

    - `searchsploit -t java`
   
![image](https://user-images.githubusercontent.com/118358126/203065407-278be3db-5b07-48d6-b7b8-678784018df6.png)
   
   If we wanted to run the exploit script `exploits/windows/remote/43993.py`, we would need to use the following Python command (**Note** - Do not actually run this command. It is just an example.):
   
   - `python exploits/windows/remote/43993.py payload=bind rhost=172.168.0.10 rport=1234 pages=/cgi-bin/status`
     
      - `python`: Command required to run Python scripts.
      - `exploits/windows/remote/43993.py`: Name of the Python exploit script.
      - `payload=bind`: The payload setting. In this example, the payload is a **bind** payload. 
          - We use a bind payload when we know the IP address of the target.
      - `rhost=172.168.0.10`: IP address of the remote host.
      - `rport=1234`: Port number of the remote host. 
      - `pages=/cgi-bin/status`: The specific page that you are trying to attack. 
      
### Summary 

  - **Exploit-DB.com** is a popular online database that contains publicly disclosed exploits, cataloged according to their **Common Vulnerability and Exposure (CVE)** identifiers.
  - **SearchSploit** is a command-line utility for Exploit-DB that allows you to take an offline copy of the entire Exploit database with you wherever you go.
    - Security professionals can perform detailed offline searches of hundreds of exploit scripts from Exploit-DB using the locally checked-out copy of the online repository.
    - SearchSploit comes preinstalled on Kali Linux and should be updated regularly. 
  - After determining which exploits to use, exploits can be attempted in the **Exploitation** phase.

## 3. Exploitation Activity

1. Refer to your past Nmap or Zenmap scans, and look in the scan results for Metasploitable2. 
   - If you cannot find it by hostname, it will be the machine with the most ports open.

![image](https://user-images.githubusercontent.com/118358126/203073079-867b305f-3c55-4cd1-a685-a036d715308f.png)

 - or type `nmap -sV 172.22.117.150` in Kali.

2. Several of these services are exploitable; however, one is exploitable with a Python script. Using `searchsploit` in Kali, search for any exploits around the service that is **listening on port 21**. You're searching for an exploit that allows you to execute a backdoor and is written in Python.

![image](https://user-images.githubusercontent.com/118358126/203073931-a6f0749f-6077-40b2-9887-57f9307f1ca2.png)

   - It's important to examine scripts before running them. Some scripts require variables to be edited within the script, whereas others can have variables passed through the command line. 
   - `searchsploit -x 49757` to search the file

3. Edit the script in nano. The path that is listed on the right is relative to the `/usr/share/exploitdb/exploit` directory, e.g., `/usr/share/exploitdb/exploit/unix/remote/xxxxx.py`.

![image](https://user-images.githubusercontent.com/118358126/203074041-874ca2a9-1010-4aa0-ab8d-11b2ad69aaf5.png)

 - `nano /usr/share/exploitdb/exploits/unix/remote/49757.py`

4. We can tell from the two variables `args` and `host` that this script accepts the IP address of the vulnerable host as an argument, so there is no need to edit the script. Close the script using ctrl+X.

![image](https://user-images.githubusercontent.com/118358126/203074273-6fe7ccdd-15d7-477f-90eb-934bcffed5a5.png)

Close the script using ctrl+X.

5. Run the script without any arguments to see the output of the script. 

    - `python /usr/share/exploitdb/exploits/unix/remote/49757.py`

    - The following image shows the script's output:

![image](https://user-images.githubusercontent.com/118358126/203074376-d3a6a6f8-4bb6-41e9-8702-780841306821.png)


6. Now, pass in the host IP address as an argument, and run the script again. You should see a message saying "Success, shell opened." Type in a Linux command to check if the shell works.

    - `python /usr/share/exploitdb/exploits/unix/remote/49757.py 172.22.117.150`

    - The following image shows the script's output:

![image](https://user-images.githubusercontent.com/118358126/203074425-5cf58dfb-1767-4011-9c67-cedf055d1413.png)

