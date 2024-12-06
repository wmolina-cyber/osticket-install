# osticket-install
# **osTicket Installation Lab**

## **Overview**
This lab demonstrates the installation and configuration of the osTicket ticketing system on a Windows-based Azure Virtual Machine. The project includes setting up the necessary dependencies, configuring IIS, and deploying osTicket for ticketing management.

## **Objectives**
- Deploy an Azure Virtual Machine (Windows 10) for hosting osTicket.
- Install and configure IIS, PHP, MySQL, and other dependencies.
- Set up osTicket for managing IT support tickets.

---

## **Steps Performed**

### **1. Azure Virtual Machine Setup**
- **VM Specifications**:
  - **Name**: `osticket-vm`
  - **OS**: Windows 10
  - **vCPUs**: 4
  - **Username**: `labuser`
  - **Password**: `osTicketPassword1!`

- **Access**:
  - Connected to the VM via Remote Desktop.

---

### **2. Download osTicket Installation Files**
- Downloaded `osTicket-Installation-Files.zip` and extracted it to the desktop, creating the folder:
  - `osTicket-Installation-Files`

---

### **3. IIS Installation and Configuration**
- Enabled IIS with the following features:
  - **World Wide Web Services**
  - **Application Development Features -> [X] CGI**

---

### **4. Install osTicket Dependencies**
- Installed the following tools from the `osTicket-Installation-Files` folder:
  1. **PHP Manager for IIS**: `PHPManagerForIIS_V1.5.0.msi`
  2. **Rewrite Module**: `rewrite_amd64_en-US.msi`

- Created the directory: `C:\PHP`
- Unzipped `PHP 7.3.8` into `C:\PHP`
- Installed **VC_redist.x86.exe**

---

### **5. MySQL Installation**
- Installed MySQL 5.5.62 (`mysql-5.5.62-win32.msi`) with the following configuration:
  - **Setup Type**: Typical
  - **Configuration Wizard**:
    - **Configuration Type**: Standard
    - **Username**: `root`
    - **Password**: `root`

---

### **6. IIS Configuration**
- Registered PHP in IIS using PHP Manager: `C:\PHP\php-cgi.exe`
- Restarted IIS (Stopped and Started the server).

---

### **7. osTicket Installation**
- Extracted `osTicket-v1.15.8.zip` and moved the `upload` folder to `C:\inetpub\wwwroot`.
- Renamed `upload` to `osTicket`.
- Restarted IIS.

- Accessed osTicket setup in the browser:
  - Navigated to: `http://localhost/osTicket/`
  - Observed missing PHP extensions.

- Enabled the following extensions in PHP Manager:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`

- Refreshed the osTicket site and verified changes.

---

### **8. Configuring osTicket**
- Renamed `ost-sampleconfig.php` to `ost-config.php`:
  - **From**: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
  - **To**: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

- Assigned permissions to `ost-config.php`:
  - Disabled inheritance and removed all permissions.
  - Granted `Everyone` full permissions.

- Completed initial setup in the browser:
  - Set helpdesk name and default email.

---

### **9. Database Configuration**
- Installed HeidiSQL from the `osTicket-Installation-Files` folder.
- Created a new session (`root/root`) and connected.
- Created a database named `osTicket`.

- Completed the osTicket browser setup:
  - **MySQL Database**: osTicket
  - **MySQL Username**: root
  - **MySQL Password**: root
  - Clicked “Install Now!”

---

### **10. Post-Installation Steps**
- Verified osTicket installation:
  - Admin Panel: `http://localhost/osTicket/scp/login.php`
  - End User Portal: `http://localhost/osTicket/`

- Cleaned up:
  - Deleted `C:\inetpub\wwwroot\osTicket\setup`.
  - Set `C:\inetpub\wwwroot\osTicket\include\ost-config.php` to read-only.

---

## **Conclusion**
This lab successfully demonstrates the deployment of a fully functional osTicket ticketing system on an Azure-hosted Windows VM, including IIS configuration, dependency installation, and database setup. This environment can now be used for managing IT support tickets.
