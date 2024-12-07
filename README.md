# osticket-install
# **osTicket Installation Lab**
![image](https://github.com/user-attachments/assets/e12bf086-5ec7-426e-9e10-adaae8de91a1)

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
![13](https://github.com/user-attachments/assets/2a0ba33e-4b96-4a44-a9f4-4ef6f7a438ca)


- **Access**:
  - Connected to the VM via Remote Desktop.
![15](https://github.com/user-attachments/assets/2c50d610-0a8a-4b4d-8dc9-45917d59a682)

---

### **2. Download osTicket Installation Files**
- Downloaded `osTicket-Installation-Files.zip` and extracted it to the desktop, creating the folder:
  - `osTicket-Installation-Files`
![22](https://github.com/user-attachments/assets/af55a998-3167-4dbd-8d50-c1170c906151)

---

### **3. IIS Installation and Configuration**
- Enabled IIS with the following features:
  - **World Wide Web Services**
  - **Application Development Features -> [X] CGI**
![30](https://github.com/user-attachments/assets/6d1bb9cf-7212-4a30-8764-b065c14d8687)

---

### **4. Install osTicket Dependencies**
- Installed the following tools from the `osTicket-Installation-Files` folder:
  1. **PHP Manager for IIS**: `PHPManagerForIIS_V1.5.0.msi`
     ![39](https://github.com/user-attachments/assets/01df0534-bf75-48a1-b511-435566b910e7)

  3. **Rewrite Module**: `rewrite_amd64_en-US.msi`
![42](https://github.com/user-attachments/assets/1141bc6e-0004-49b7-b992-b214f17dd40c)

- Created the directory: `C:\PHP`
- Unzipped `PHP 7.3.8` into `C:\PHP`
- Installed **VC_redist.x86.exe**
![56](https://github.com/user-attachments/assets/d26bfdde-9163-4bc7-8dc1-10b62906acdc)

---

### **5. MySQL Installation**
- Installed MySQL 5.5.62 (`mysql-5.5.62-win32.msi`) with the following configuration:
  - **Setup Type**: Typical
  - **Configuration Wizard**:
    - **Configuration Type**: Standard
    - **Username**: `root`
    - **Password**: `root`
![68](https://github.com/user-attachments/assets/d871fa4c-fe51-425c-a8a8-9e7d5b959bf9)

---

### **6. IIS Configuration**
- Registered PHP in IIS using PHP Manager: `C:\PHP\php-cgi.exe`
- Restarted IIS (Stopped and Started the server).
![76](https://github.com/user-attachments/assets/facba375-8cf0-48c5-8902-44edf64738d5)

---

### **7. osTicket Installation**
- Extracted `osTicket-v1.15.8.zip` and moved the `upload` folder to `C:\inetpub\wwwroot`.
- Renamed `upload` to `osTicket`.
- Restarted IIS.

- Accessed osTicket setup in the browser:
  - Navigated to: `http://localhost/osTicket/`
  - Observed missing PHP extensions.
![95](https://github.com/user-attachments/assets/c294d51c-2c44-43cd-a524-fbd98500c6a2)

- Enabled the following extensions in PHP Manager:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`
![102](https://github.com/user-attachments/assets/d4a49e9d-cfc1-40bf-9228-cd131b68e4bd)

- Refreshed the osTicket site and verified changes.

---

### **8. Configuring osTicket**
- Renamed `ost-sampleconfig.php` to `ost-config.php`:
  - **From**: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
  - **To**: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`
![109](https://github.com/user-attachments/assets/d31ba877-e431-4f9c-a52e-2ec8ffe30573)

- Assigned permissions to `ost-config.php`:
  - Disabled inheritance and removed all permissions.
    ![115](https://github.com/user-attachments/assets/313a1dc5-94b6-40fe-904c-2740b8b1d02a)

  - Granted `Everyone` full permissions.
   ![120](https://github.com/user-attachments/assets/1af3e9e8-af55-49e7-ba0d-9c62d274afb8)


- Completed initial setup in the browser:
  - Set helpdesk name and default email.
![123](https://github.com/user-attachments/assets/0ced43da-d5d0-4ac8-b907-dd02af4d3c0f)

---

### **9. Database Configuration**
- Installed HeidiSQL from the `osTicket-Installation-Files` folder.
  ![130](https://github.com/user-attachments/assets/e28b287c-ef0b-4c37-b288-ac405156e1bd)

- Created a new session (`root/root`) and connected.
  ![133](https://github.com/user-attachments/assets/6d179f79-2d6f-406d-af1b-04cd8017049b)

- Created a database named `osTicket`.
  ![135](https://github.com/user-attachments/assets/698dda31-804d-442a-92b8-6d0d1cc9188a)

- Completed the osTicket browser setup:
  - **MySQL Database**: osTicket
  - **MySQL Username**: root
  - **MySQL Password**: root
  - Clicked “Install Now!”
![136](https://github.com/user-attachments/assets/56e58afe-53a9-4372-8f6a-9b374416790f)

---

### **10. Post-Installation Steps**
- Verified osTicket installation:
  - Admin Panel: `http://localhost/osTicket/scp/login.php`
    ![139](https://github.com/user-attachments/assets/f44fc196-1965-4e49-8e44-c1712ce92a1a)

  - End User Portal: `http://localhost/osTicket/`
    ![140](https://github.com/user-attachments/assets/3497bbb7-cd68-41f7-9ce5-a0ed30846831)


- Cleaned up:
  - Deleted `C:\inetpub\wwwroot\osTicket\setup`.
  - Set `C:\inetpub\wwwroot\osTicket\include\ost-config.php` to read-only.

---

## **Conclusion**
This lab successfully demonstrates the deployment of a fully functional osTicket ticketing system on an Azure-hosted Windows VM, including IIS configuration, dependency installation, and database setup. This environment can now be used for managing IT support tickets.
