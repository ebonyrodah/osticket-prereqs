# osticket-prereqs
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

   ### **1. Operating system**
   - Windows 10, Windows server 2012 or newer
   ### **2. Web server**
   - IIS (Internet Information Services) version 7 or newer incase you are using windows.
   - Apache version 2.4 or newer if you are using linux.
   ### **3. PHP**
   - Supported versions: PHP 7.2 to 8.1 (osTicket 1.15.8 is compatible with these)
   - Enable PHP extentions,examples of the ones that will be enabled are;
     - **php_imap.dll**: for fetching and sending emails.
     - **php_intl.dll**: For internationalization support.
     - **php_opcache.dll**: For performance optimization.
   ### **4. Dependencies and Tools**
   - PHP manager for IIS : PHP Manager simplifies configuring and managing PHP for IIS.
   - URL rewrite module  : It helps in creating clean URLs and improves SEO and user experience.
   - Microsoft Visual C++ Redistributable : this is normally required for running PHP.
   - HeidiSQL(Optional) : Used by backend administrators to connect to the MYSQL database that osTicket uses.
   ### **5. osTicket Software**
   - Download the latest stable release of osTicket (osTicket-v1.15.8).
   ### **6. Browser Access**
   - A modern web browser (e.g., Chrome, Firefox, Edge) to access and configure osTicket via its web interface.
   ### **7. Hardware Requirements**
   - Memory : Atleast 2 GB minimum (4 GB or more recommended for larger environments).
   - Processor : Minimum 2 GHz (recommendation: multi-core).
   - Storage : At least 10 GB free space for the operating system, database, and attachments.



<h2>Installation Steps</h2>
Here are the steps that i used to download the osTicket and some of the tools i used.

### **1. Set Up the Virtual Machine in Azure**
a. **Create a VM in Azure**:
   - Go to Azure first create a resource  group then continue by creating a **Windows 10** virtual machine with:
     - Name: **osticket-vm**
     - Size: **4 vCPUs** (this is like the computer’s brain capacity).
     - Username: **labuser**
     - Password: **osTicketPassword1!**
   - Finish creating the VM.

<p>
<img src="https://i.imgur.com/Ko7t7M2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

    

       
---


2. **Connect to the VM**:
   - Once the deployment of the virtual machine is complete go and copy the public ip address which will be used to log into it together 
     with the username and password.
   - Download the **Remote Desktop (RDP)** file from Azure.
   - Open it, log in using:
     - Username: **labuser**
     - Password: **osTicketPassword1!**
</p>
<br />

<p>
<img src="https://i.imgur.com/6kVEcT6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>



---


### **3. Prepare the Files**
a. **Download the Setup Files**:
   - Inside the VM, download the `osTicket-Installation-Files.zip`.
   - Extract (unzip) it to your Desktop. Name the folder **osTicket-Installation-Files**.
</p>
<br />

<p>
<img src="https://i.imgur.com/xNP1WMQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>



---


### **3. Set Up Windows Features**
a. **Enable IIS (Internet Information Services)**:
   - Open **Control Panel** > **Programs** > **Turn Windows features on or off**.
   - Find **Internet Information Services** (IIS).
   - Expand **World Wide Web Services** > **Application Development Features**.
   - Check the box for **CGI**, then click OK. This sets up the system to run websites.
   - Expand **common HTTP features** check all the boxes then click ok, after this the installation of IIS will start.
</p>
<br />

<p>
<img src="https://i.imgur.com/Dd96gYK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>



---


### **4. Confirmation of IIS working**
a. Go to your browser search **127.0.0.1** click enter then it will load a page image, this confirms that **IIS** has been installed and 
   is fully funtional

</p>
<br />

<p>
<img src="https://i.imgur.com/8cnG66h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>



---


### **5. Setting up Tools and Softwares that osTicket will use**
1. **Go to osTicket installion files and start downloading the files in this order:**
   - **Install PHP manager**: Double click the file `PHPManagerForIIS_V1.5.0.msi`to install.
   - **Install Rewrite Module**: Double-click `rewrite_amd64_en-US.msi`to install.
   - **Set Up PHP**:
     - Create a directory in PHP, Go to `Local Disk(C:)` create a folder and name it `C:\PHP`.
     - From the installation files download `php-7.3.8-nts-Win32-VC15-x86.zip` and extract the contents into `C:\PHP`.
   - **Install Visual C++ Redistributable**:  Double-click `VC_redist.x86.exe` to install.
   - **Install MYSQL**:
     - Double click `mysql-5.5.62-win32.msi` to install MySQL( this osTicket's database)
     - click the `Typical setup` option
     - In the setup wizard choose `Standard Configuration`
     - Setup password as **password!** and username as **root**
</p>
<br />

<p>
<img src="https://i.imgur.com/ffis4gd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>



---


### **6. Configure IIS**
1. **Register PHP with IIS**:
   - Open IIS (search for “IIS Manager” on the Start menu right click and select run as administrator).
   - Go to **PHP Manager** and register PHP:
     - Path: `C:\PHP\php-cgi.exe`.
   - Restart IIS (click **Stop**, then **Start** the server in IIS).
2. **Install osTicket**:
   - Go to the`osTicket-Installation-Files` folder.
   - Double click the `osTicket-v1.15.8.zip` which will redirect you to the `Upload` folder.
   - Copy the `Upload` folder to ``C:\inetpub\wwwroot`.
   - Once pasted rename `Upload` folder to **`osTicket`**
3. **Open osTicket in a Browser**:
   - Go back to IIS and restart it.
   - In **Sites -> Default -> osTicket**, click **Browse *:80**.
   
</p>
<br />

<p>
<img src="https://i.imgur.com/MzplTSV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
</p>
<p>
- In the image you will notice some missing extensions which will be enabled.




---


### **7. Enable PHP Extensions**:
   - In IIS, go to **PHP Manager** > **Enable or disable an extension**.
   - Enable:
     - `php_imap.dll`
     - `php_intl.dll`
     - `php_opcache.dll`.
   - Restart IIS and refresh the osTicket page.

</p>
<br />

<p>
<img src="https://i.imgur.com/47FQxhk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

