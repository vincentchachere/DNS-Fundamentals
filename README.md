<br>

<p align="center">
<img width="700" src="https://github.com/user-attachments/assets/9b6b0a51-6411-4e01-96c5-1bb31e6fd986" alt="Microsoft Active Directory Logo"/>
<br>

<br>

<br>

<h1 align="center">DNS Fundamentals</h1> 
<br>

<p align="center">
<img src="https://github.com/user-attachments/assets/5e09d8e2-b1a0-4ddd-801d-9be7fe6cbb1c" height="50%" width="50%" alt="9"/><br />
</p>
<br />

## Lab Overview

This lab builds on the previous one [here](https://github.com/vincentchachere/Active-Directory-Deployment-and-Configuration). This lab focuses on understanding and practicing DNS record management and behavior in a controlled environment. We will work with A-records, CNAME records, and local DNS cache management to observe how DNS changes affect network communication.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services (AD DS)
- DNS Management Console
- PowerShell

## Operating Systems Used

- Windows Server 2022
- Windows 10 (21H2)

## High-Level Group Policy and Account Managing Steps

- A-Record Management
- Local DNS Cache Management
- CNAME Record Configuration

## Configuration Steps

<details>

<summary>

### 📂 Exercise 1: A-Record Management

</summary>

*Log into DC-1 as your domain admin account; **mydomain.com\jane_admin***

*Additionally, log into Clinet-1 as an admin; **mydomain.com\jane_admin***

- From Client-1 try to ping: `mainframe` (notice that it fails)

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

- Nslookup: `mainframe` (*notice that it fails, because there's no DNS record.*)

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

Create a **DNS A-record** on **DC-1** for **mainframe** and have it point to **DC-1’s Private IP address** (*10.0.0.4*)

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

Return to **Client-1** and **ping** it to confirm functionality.

<img width="800" alt="isolated" src="">

</details>

<details>

<summary>

### 📂 Exercise 2: Local DNS Cache Management

</summary>

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<img width="800" alt="isolated" src="">

</details>

<details>

<summary>

### 📂 Exercise 3: CNAME Record Configuration

</summary>

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<img width="800" alt="isolated" src="">

<br>
<br>
<br>

<img width="800" alt="isolated" src="">

</details>
