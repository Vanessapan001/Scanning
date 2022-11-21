# Nmap

For scanning networks to discover what hosts are present and what services are available on those hosts, we will be using the Nmap tool loaded into Kali.

1.1 `nmap -sn`

Sub-net scan, it's using the ICMP ping protocol to see whether it responds.

![image](https://user-images.githubusercontent.com/118358126/202834409-e05da7e7-bd80-436a-a966-24e9f601936a.png)

![image](https://user-images.githubusercontent.com/118358126/202834433-ebbc3b39-b2f7-49b4-accc-cab74a633f17.png)

![image](https://user-images.githubusercontent.com/118358126/202834442-1ff2778e-976e-4a76-a434-6f55d375415e.png)

Nmap is checking the most common services to see if they’re open on the host. It does this by starting to open a connection to the service, and then closing it down before the connection is complete. This is called a TCP SYN ping, and it works by sending an empty TCP packet with the SYN flag set and waiting for the host to respond with the standard SYN-ACK response. While a normal connection would be completed by sending back an ACK, Namp instead cancels the connection before it complete.

1.2 `nmap -sU`
This will check the most common thousand UDP ports.
we can add the -P0 option to skip the ping check of the host.

![image](https://user-images.githubusercontent.com/118358126/202834530-bcf8e700-461d-47d8-870e-990f81c2e588.png)

1.3 `nmap -sV`
Nmap will try to identify the version of software being used for the service.
`-p` - to limit the test just on 1 service.
`-p22` - only scan the port 22/tpc

![image](https://user-images.githubusercontent.com/118358126/202834783-58c6efd2-6e9c-43e2-a2be-64ab0ac46fb3.png)

1.4 `nmap -sSUV` specifies both TCP and UDP and service detection.

`nmap -p` requests the UDP ports 53, 111,137, and TCP ports 21 to25, 80, 139, 8080

![image](https://user-images.githubusercontent.com/118358126/202834909-d0d7e47a-398a-4d20-958c-f48dfe6f4f5a.png)

![image](https://user-images.githubusercontent.com/118358126/202834915-54818cd3-8448-48e3-9cc3-c40d43059954.png)

1.5 `nmap -O` to see what operation system is on the target.

![image](https://user-images.githubusercontent.com/118358126/202834946-a80484fd-74e9-4460-b65e-d82904c92bfd.png)

![image](https://user-images.githubusercontent.com/118358126/202834959-3791478a-c6a8-4264-9a4c-c5c0b9ae19f5.png)

1.6	Nmap also has a comprehensive library of scripts.

![image](https://user-images.githubusercontent.com/118358126/202835244-17fb25d3-e6e6-49de-b465-fe719bc880a9.png)

![image](https://user-images.githubusercontent.com/118358126/202835249-e87afb1a-53d4-4197-9f02-c05bccee3edf.png)

1.7 we will use the rexec brute force test to extract credentials via port 512.
We can do this by using the `–script` argument.
Here we see a list of valid credentials for the Metasploitable server.

![image](https://user-images.githubusercontent.com/118358126/202835279-2adff0c6-d518-4f3e-93bc-c015d41f6127.png)

![image](https://user-images.githubusercontent.com/118358126/202835283-80cd6459-ce7b-4455-9fc7-c4e04c0f3b6f.png)


