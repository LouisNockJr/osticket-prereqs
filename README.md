<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.
<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- Remote Desktop Application on either Windows or [MacOS](https://apps.apple.com/us/app/windows-app/id1295203466?mt=12)
- [osTicket Installation Files](https://github.com/osTicket/osTicket/releases)

<h2>Installation Steps</h2>

<p>
<img src="https://imgur.com/zDWiACb" height="80%" width="80%" alt="Virtual Machine Setup"/>
</p>
<p>
🖥️ Step 1: Create and Access the Virtual Machine

- Create an Azure Virtual Machine with the following specs:
  - **OS**: Windows 10
  - **vCPUs**: 4
  - **Name**: `osticket-vm`
  - **Username**: `labuser`
  - **Password**: `osTicketPassword1!`
- Connect via **Remote Desktop (RDP)** to the Public IP Address given to the VM in Azure
  - On Mac, use the Windows App
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
📦 Step 2: Prepare the Environment
  
- Download and unzip `osTicket-Installation-Files.zip` to the Desktop.
- Enable **IIS with CGI**:
  - Go to `Control Panel > Programs > Turn Windows features on or off`
  - Enable:
     ```
     [X] Internet Information Services
         [X] Web Management Tools
         [X] World Wide Web Services
             [X] Application Development Features
                 [X] CGI
     ```
- From the `osTicket-Installation-Files` folder, install:
  - `PHPManagerForIIS_V1.5.0.msi`
  - `rewrite_amd64_en-US.msi`
- Create a new folder: `C:\PHP`
- Extract `php-7.3.8-nts-Win32-VC15-x86.zip` into `C:\PHP`
- Install `VC_redist.x86.exe`
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
🛠️ Step 3: Install MySQL and Configure PHP

- Install `mysql-5.5.62-win32.msi`:
  - Choose **Typical Setup**
  - Launch Configuration Wizard
  - Select **Standard Configuration**
  - Set credentials:
    - **Username**: `root`
    - **Password**: `root`

- Open **IIS Manager as Administrator**:
  - Use **PHP Manager** to register PHP:
     ```
     C:\PHP\php-cgi.exe
     ```
  - Restart IIS (Stop/Start)

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
🌐 Step 4: Install and Configure osTicket

- Extract `osTicket-v1.15.8.zip` from the files folder.
- Copy the `upload` folder to: C:\inetpub\wwwroot
  - Rename `upload` to `osTicket`

- Reload IIS and browse: IIS > Sites > Default Web Site > osTicket > Browse *:80

- Enable required PHP extensions:
  - In **PHP Manager**, click:
    ```
    Enable or disable an extension
    ```
  - Enable:
    - `php_imap.dll`
    - `php_intl.dll`
    - `php_opcache.dll`

- Rename config file:
  - From:
    ```
    C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
    ```
  - To:
    ```
    C:\inetpub\wwwroot\osTicket\include\ost-config.php
    ```

- Set permissions:
  - Disable inheritance
  - Remove all existing
  - Add: `Everyone` with **Full Control** 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
🧩 Step 5: Final Setup and Database Configuration

- In your browser, start the osTicket setup:
  - Helpdesk Name
  - Default email

- Install **HeidiSQL** and open it
  - Connect using:
    - **Username**: `root`
    - **Password**: `root`
  - Create a database:
    ```
    osTicket
    ```

- Return to the browser and complete the install:
  - **MySQL Database**: `osTicket`
  - **MySQL Username**: `root`
  - **MySQL Password**: `root`
  - Click **Install Now**


✅ Access Your Help Desk

- Admin URL: [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
- User URL: [http://localhost/osTicket/](http://localhost/osTicket/)
</p>
<br />
