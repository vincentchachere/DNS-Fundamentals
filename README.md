<br>

<p align="center">
<img width="700" src="https://github.com/user-attachments/assets/9b6b0a51-6411-4e01-96c5-1bb31e6fd986" alt="Microsoft Active Directory Logo"/>
<br>

<br>

<br>

<h1 align="center">DNS Fundamentals - Lab Overview</h1>

This lab builds on the previous one [here](https://github.com/vincentchachere/Active-Directory-Deployment-and-Configuration). This lab focuses on understanding and practicing DNS record management and behavior in a controlled environment. We will work with A-records, CNAME records, and local DNS cache management to observe how DNS changes affect network communication.

<p align="center">
<img src="https://github.com/user-attachments/assets/a17b7f35-f05e-4eb4-886e-a7f3940f31fd" height="50%" width="50%" alt="9"/><br />
</p>

<h2 align="center">DNS Resolution Process</h2>

<ins>When a computer tries to interact with a hostname, it resolves it through the following steps</ins>:

1. **Local DNS Cache**: The computer first checks its DNS cache stored in memory (fastest).
2. **Hosts File**: If not found in the cache, it checks the local `hosts` file (faster).
3. **DNS Server**: If unresolved, it queries the configured DNS server (slowest, usually provided by your ISP or manually configured).

   - **Recursive Resolver**: The DNS server (resolver) checks its own cache.

   - **Root Server**: If the resolver doesn’t have the answer, it queries a root server to locate the top-level domain (TLD) server (e.g., .com, .org).

   - **TLD Server**: The root server directs the resolver to the authoritative TLD server for the domain.

   - **Authoritative Name Server**: The TLD server directs the resolver to the domain's authoritative name server, which provides the IP address of the hostname.

4. **Response and Caching**: The resolver sends the IP address back to the computer and caches the result for future requests.

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

*Additionally, log into Client-1 as an admin; **mydomain.com\jane_admin***

- From Client-1 Open: `PowerShell`

- Ping: `mainframe` (notice that it fails)

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/fccfc3e1-cd3e-4412-aaf0-6ee17efc42d2">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

To view DNS records, run the command **`ipconfig /displaydns`**, which displays them in the console.

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/06646f25-0608-4032-b0e2-ceb3991284c8">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

To verify there are no DNS records for **mainframe**, output the results to a text file and search for "mainframe" to confirm it is absent from the local DNS cache.

- Run the Command: `ipconfig /displaydns > test.txt` (*This command saves the DNS records to a text file that can be opened in Notepad.*)

- Run the Command: `notepad test.txt` (*This command opens the specified text file in Notepad.*)

- Press: `Ctrl + F` (For Windows) and `Command + F` (For Mac) to open the "Find" window and search for the DNS Record "mainframe"

*Since there's no A-Record for "mainframe," the search will return no results.*

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/64578e00-4df8-4122-aac3-f3150604d6b3">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

I will now show you where the local host file is, so first open notepad **as an administrator**.

- Go To: `This PC` > `Windows (C:) > `Windows` > `System32` > `drivers` > `etc`

- Select: `hosts` (*this is the hosts file*) and **Open it with Notepad**

*You will see it populate inside Notepad.*

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/aeaf6a94-7ab8-4916-b3c5-86fa3b706b13">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

So to briefly practice let's try to **ping elephant**. Notice that will fail, since it's not in the hosts file. Now, if we...(to be continued)

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
