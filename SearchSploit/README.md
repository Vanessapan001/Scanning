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
