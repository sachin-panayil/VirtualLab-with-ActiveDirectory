# Home Lab Setup using Virtual Box and Active Directory

## Overview

This project shows the configuration of a home lab environment using Virtual Box to create a simulated network infrastructure with Windows 10 and Windows Server 2019 virtual machines.

## Steps

### 1. Installations

- Installed Virtual Box.
- Installed Windows 10 ISO and Windows Server 2019 ISO.

### 2. Virtual Machine Setup

- Established a new virtual machine named 'DC' to serve as the domain controller, running Windows Server 2019.
- Set up a new virtual machine named 'CLIENT1' to function as a client machine, operating on Windows 10 Pro.

### 3. IP Address Configuration

- According to the network diagram, the domain controller is equipped with two network adapters: one for the home internet connection ('INTERNET') and another for the internal network ('INTERNAL') that client machines will join.
- Labeled my home network adapter as 'INTERNET' and the internal network adapter as 'INTERNAL'.
- Configured the IPv4 properties for the internal network adapter with the IP address 172.16.0.1, a subnet mask of 255.255.255.0, and the DNS server set to 127.0.0.1 (loopback address).

### 4. Active Directory Domain Services

- Installed Active Directory Domain Services using Server Manager.
- During configuration, set up a new forest named 'mydomain.com'.
- This process transformed the virtual machine into a domain controller.

### 5. Active Directory Users and Computers

- Created a new organizational unit and set up a new administrator account.
- Modified the properties of the new user to include it as a member of 'Domain Admins'.
- Signed out and then signed in using the newly created domain admin account.

### 6. Configuring Remote Access and DHCP Server

(This configuration allows the Windows 10 client to access the internet via the domain controller while being on the private internal network.)

- Installed Remote Access through Server Manager, ensuring the routing service was selected.
- Set up routing and remote access and configured NAT (Network Address Translation) to use my home network for internet access.
- Installed DHCP via Server Manager, enabling automatic IP address assignment to clients on the network.
- Created a new scope to allocate IP addresses within the range of 172.16.0.100-200 to clients.

### 7. PowerShell Script for Creating Users

- Utilized a public script by Josh Madakor, available on [GitHub](https://github.com/joshmadakor1).
- Opened an elevated PowerShell window, navigated to the folder containing the unzipped script, and executed it to create approximately 1000 users in an organizational unit named '_USERS', simulating a corporate environment.

### 8. Onboarding the Client Machine

- Configured the network settings of the client machine in VirtualBox to 'internal network'.
- Started the machine, used `ipconfig`, and pinged a website in Command Prompt to verify network settings.
- Accessed system properties on the client machine to join the domain 'mydomain.com' and signed in with a previously created account.
- Verified the client machine's address lease in the DHCP - Address Leases on the domain controller.
- Observed the computer name under Active Directory Users and Computers - Computers.


