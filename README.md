<br>

<p align="center">
<img width="700" src="https://github.com/user-attachments/assets/9b6b0a51-6411-4e01-96c5-1bb31e6fd986" alt="Microsoft Active Directory Logo"/>
<br>

<br>

<br>

<h1 align="center">DNS Resolution</h1>

Building on the previous [Active Directory Deployment and Configuration](https://github.com/vincentchachere/Active-Directory-Deployment-and-Configuration) lab, this lab provides hands-on experience in DNS record management, where participants will configure and manage A-records and CNAME records. It also covers local DNS cache management to demonstrate how DNS changes affect network communication and troubleshooting. Through this lab, users will gain a deeper understanding of DNS functionality and its impact on the resolution of domain names and network connectivity.

<p align="center">
<img src="https://github.com/user-attachments/assets/75b66a42-6744-4727-809c-11f0401160b4" height="50%" width="50%" alt="9"/><br />
</p>

<h2 align="center">DNS Resolution Process</h2>

<ins>When a computer tries to interact with a hostname, it resolves it through the following steps (*explaining the image above*)</ins>:

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

## High-Level DNS Resolution Steps

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

To practice, let's **ping elephant**. It will fail since it's not in the `hosts` file. After adding "elephant" to the loopback address (127.0.0.1) and saving, the ping will succeed.

*You may need to add your domain admin account (`domain.com\jane_admin`) to the **hosts properties** > **Advanced** > **Add** > **Add: Jane Doe (Domain Admin Account)** > **OK** to grant the necessary permissions and save the file.*

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/da52b240-2359-4e87-914f-f64d1d900f50">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

Let's try to nslookup "mainframe." Then, in the next step, we'll create a DNS A-record on DC-1 for "mainframe" and have it point to DC-1's private IP address, in order to successfully resolve the domain name.

- Nslookup: `mainframe` (*notice that it fails, because there's no DNS record.*)

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/eb41a84d-b7bb-4b0a-a791-5a26aa7dfbd0">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

Create a **DNS A-record** on **DC-1** for **mainframe** and have it point to **DC-1’s Private IP address** (*10.0.0.4*)

*Inside DC-1*

- Click Start and Exapnd Windows Administrative Tools then Select: `DNS`

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/cf02dfbd-6c65-4769-a02f-392b8359a498">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

*Inside DNS Manager expand **DC-1** and **Forward Lookup Zones** then select **mydomain.com**. Next, right click an empty space and select **New Host (A or AAAA)**.*

- New Host Name: `mainframe`

- IP Address: `DC-1's Private IP Address` (*Example: 10.0.0.4*)

- Select: `Add Host`

*Notice mainframe immediately populates within the mydomain.com folder.*

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/f339a9e2-d445-43ab-ba30-6e8081ebbfe4">

<br>
<br>
<br>

<ins>A-Record Management</ins>:

Return to **Client-1** and ping **mainframe** to confirm functionality. Then, try an **nslookup** for **mainframe**.  

*With the DNS A-record now created on DC-1, both the ping and nslookup will succeed.*

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/b5c51ea9-4207-4d26-b8f0-a1a6dd0668ec">

</details>

<details>

<summary>

### 📂 Exercise 2: Local DNS Cache Management

</summary>

For this part we will go back to **DC-1** and **change mainframe’s record address** to **8.8.8.8**.

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/e9914f50-dd11-42ba-8b5a-6793bea43c9a">

<br>
<br>
<br>

<ins>Local DNS Cache Management</ins>:

Now, if we ping **mainframe**, it will still show DC-1's private IP address. In the next step, we'll **open PowerShell as an Administrator** and **flush the DNS** to link the new IP address (8.8.8.8) with **mainframe** in the **host** file.  

*The word "elephant," previously linked to Client-1's loopback address, is also present here.*

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/254dd51b-48c7-43e1-a6d0-252bdd1e5c8d">

<br>
<br>
<br>

<ins>Local DNS Cache Management</ins>:

After opening **PowerShell as an administrator** and flushing the Local DNS Cache, you can observe the new IP address (8.8.8.8) assigned to **mainframe** and the previously created "elephant" domain. Running **nslookup** for **mainframe** will also show the updated IP address.

<ins>The process the computer went through to achieve this was as follows</ins>:  

1. The computer checked the **Local DNS Cache** (fastest), but since it was flushed, nothing was found.  
2. It then checked the **Local Hosts File** (faster), but there was no entry for **mainframe**.  
3. Finally, the computer queried the **DNS Server** (slowest) and retrieved the new IP address for **mainframe**.  

*This entire DNS resolution process occurs within milliseconds.*

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/6b1d7d4a-84fc-4571-b335-a07af4a60f17">

</details>

<details>

<summary>

### 📂 Exercise 3: CNAME Record Configuration

</summary>

On **DC-1**, create a **CNAME record** to point the host **search** to **www.google.com**. Next, we'll attempt to ping the newly created "search" CNAME record and observe the results.

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/c51bf473-1e6b-4623-a7b0-f32d10bd1aa0">

<br>
<br>
<br>

<h3 align="center">This Concludes the Fundamentals of DNS Resolutions Lab!</h3>

<ins>Observing the CNAME Record</ins>

Once back inside Client-1, **ping** and **nslookup** "search" to observe the results. Notice that the IP address for "search" resolves to the same IP as "www.google.com."

<img width="800" alt="isolated" src="https://github.com/user-attachments/assets/f3cd0ca0-ca20-4e3c-a1d4-21c7ef06788f">

</details>

<h2 align="center">Final Thoughts</h2>

This lab covered fundamental DNS concepts, including creating and managing A-records, working with local DNS cache, and configuring CNAME records. We practiced troubleshooting DNS resolution, observed how changes propagate, and reinforced key skills for managing DNS in real-world environments.

Next, we’ll build on this lab with the [Network File Shares and Permissions](https://github.com/vincentchachere/Network-File-Shares-and-Permissions) lab.

Thank you for following along with this project. Your time and effort in learning and implementing these concepts are greatly appreciated.

☎️ For questions or to connect you can reach me at: www.linkedin.com/in/vincentchachere
