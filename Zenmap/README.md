# Zenmap

## Nmap and Zenmap

We will now demonstrate how to use the scanning tools Zenmap and Nmap.

In this demonstration, you'll complete the following steps:
  - Use Nmap to perform a port scan on an internal network.
  - Introduce a GUI alternative to Nmap called Zenmap. 
  - Use Zenmap to perform a port scan and highlight additional features offered. 

To performing a port scan on the internal network, complete the following steps:

1. Open a terminal, and look up your IP address by typing `ip addr`, as the following image shows:
	
![image](https://user-images.githubusercontent.com/118358126/202978726-7f11d44f-e395-4899-83d3-3f2f47e0d2d3.png)
	
2. Using the IP address under `eth0`, perform an Nmap scan against the network using the /24 CIDR, as the following image shows:
	
![image](https://user-images.githubusercontent.com/118358126/202979528-54d97e99-ed24-492c-bf24-63ca2fa653aa.png)

## Zenmap

1. Nmap's GUI application is called **Zenmap**. 

2. Zenmap is inbuilt in Kali

3. It provides an easy-to-use tool to automate scanning tasks.

4. Open a terminal and type `zenmap`.

5. Note the fields at the top of the application: 

    - **Target** is where we input a hostname or IP address. CIDR notation is also accepted.

    - **Profile** is a drop-down menu that contains several pre-built scans. These can be changed and edited. You can also create custom profiles. 

    - **Command** shows the Nmap command being run. This will update automatically if we change or edit a profile.

6. Begin by selecting the **Intense scan** profile.

    - Select **Intense scan** from the drop-down menu next to **Profile**.

    - Note that our **Command** field has changed to `nmap -T4 -A -v`. 

       - `-T4` is used to increase the scan speed. 

       - `-A` includes OS and version detection, script scanning, and traceroute.

       - `-v` is level 1 of verbose, which shows status updates as the scan progresses.

7. Next, we will edit this intense scan profile.

    - At the top, select **Profile**, as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/202980292-c9e9bfc6-f28e-4f38-9740-4967bebdfb3a.png)

- Then, select **Edit Selected profile**.

- Click the **Scripting** tab at the top of the screen, as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/202980471-9c368dbe-1ac5-43f7-8194-ede04c6d01e7.png)

   - This tab will display a list of NSE scripts. 

      - **Nmap scripting engine (NSE)** scripts are scripts written in the programming language LUA. They perform an action on a desired port or service. 

      - NSE scripts are commonly used to test whether a service is vulnerable to an exploit. 

      - By default, Zenmap's intense scan uses some basic NSE scripts. However, we'd like to add additional scripts to our scan.

8. We'll select a few of the many NSE scripts listed in the Scripting tab. What scripts we decide to run typically depends on the discovered ports and services of the host. (It's better to do a regular port scan or version scan first to determine what ports are open, then perform another Nmap scan with NSE scripts selected.)

    - Select **smb-os-discovery** and **smb-system-info** toward the bottom of the list, as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/202980906-374d9a82-431c-4f48-ad3e-83785d3b519d.png)

9. Save the profile, and then enter the network range IP in the **Target** box and click **Scan**.

10. Let the scan finish, and scroll down to the machine with port 445 open, as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/202981155-1f7b3fca-683e-4589-9956-255191e2e75d.png)

- The NSE scripts that we selected performed additional scanning on the SMB service. This provided more information, which ultimately confirmed that the machine is a Windows 10 machine.


## Zenmap Activity

### Instructions

1. In Kali, launch Zenmap by typing `zenmap` in the terminal.

2. Ensure that "Intense scan" is selected next to "Profile," as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/202982172-67ff25c4-1f0a-4485-a8d8-b463a74cd312.png)

Navigate to "Profile" > "Edit Selected Profile" to read about the intense scan profile.

3. Click "Cancel," as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/202982257-ca4c82c0-ea8e-41e6-bca0-bd12d60b9ab5.png)

4. Type in your subnet's IP range using CIDR notation (e.g., /24), and click "Scan." Wait for the scan to finish, and view the results. There is a machine of interest that has port 21 open; take note of its IP address.

![image](https://user-images.githubusercontent.com/118358126/202988080-f0837093-b51e-4f2b-8bac-1951ed19ab56.png)

5. Intense scan automatically uses certain NSE scripts based on the services discovered via the `-sC` flag. To add additional scripts, go to "Profile" > "Edit profile" > "Scripting," as the following image shows:

![image](https://user-images.githubusercontent.com/118358126/202982356-8c1d20f6-38ea-4786-9a75-cf7f127fb13d.png)

6. Scroll down to "ftp" and add "ftp-vsftpd-backdoor." Click "Save Changes." 

![image](https://user-images.githubusercontent.com/118358126/202982622-8bc6d426-2176-4538-862c-9f81e6bd7ac9.png)

7. Now the intense scan profile has been edited to include these NSE scripts. In the "Target" box, enter the IP address of the machine with port 21 open, and click "Scan" to re-run the scan on that specific host.

8. Notice in the output that port 21 (FTP) is vulnerable to the backdoor exploit.

![image](https://user-images.githubusercontent.com/118358126/202988236-1edce147-d662-42ff-a431-b8684afda520.png)

9. Save this scan by going to "Scan" > "Save Scan."
