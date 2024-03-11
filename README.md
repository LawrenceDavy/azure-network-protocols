<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<hr>
<br>

<h2>1. Create some sample file shares with various permissions</h2>

![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/a2ca95f7-0dd1-48e0-aeeb-e5234d315d5b)
![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/45581ba1-3662-4305-9a5d-84c708fab621)
![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/18cef67a-d718-4853-8b2e-71dd89a86022)
![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/915283e0-3279-4061-a5c1-ae294c5eec25)
- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
- Connect/log into Client-1 as a normal user (mydomain\<someuser>)
- On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
- Set the following permissions (share the folder) for the “Domain Users” group:
  - Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
  - Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
  - Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”

<hr>
<br>

<h2>2. Attempt to access file shares as a normal user</h2>

![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/51dc19f0-cf3c-40f6-8eda-baccfd498f25)
![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/8245dd74-6e80-4d3d-97ea-0146e5d5e416)
- On Client-1, navigate to the shared folder (start, run, \\dc-1)
- Try to access the folders you just created. You realise that you can access "read-access" and "write-access" folders but denied access to "no-access" folder due to lack of privileges as a  normal user

<hr>
<br>

<h2>Create an “ACCOUNTANTS” Security Group, assign permissions, an test access</h2>

![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/4126120c-9fa0-4edf-bb25-76a8f7a1214f)
- Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/3715f4d5-2c48-4479-b2c6-3d73fbbd7cb2)
- On the “accounting” folder you created earlier, set the following permissions:
- Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”

![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/4bbd21ac-c34a-49c6-a61e-12c856937fd7)

![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/40a1b6ce-a5e4-4b02-8a78-8bc5a75ee763)

![image](https://github.com/LawrenceDavy/configure-ad/assets/24421979/c932972e-ce38-4d9d-a0f8-765ca033819e)
