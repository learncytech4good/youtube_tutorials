# Splunk Lab Environment Setup

This guide provides step-by-step instructions for setting up a lab environment using VirtualBox, CentOS, and Splunk Enterprise on a Linux platform.

## VirtualBox Download & Installation

1. Go to [VirtualBox](https://www.virtualbox.org/) official website.
2. Click on the "Downloads" section.
3. Choose the appropriate version for your operating system and download the installer.
4. Run the installer and follow the on-screen instructions to install VirtualBox.

## CentOS Download

1. Visit the [CentOS download page](https://www.centos.org/download/).
2. Choose the CentOS version you want (e.g., CentOS 7 or CentOS 8).
3. Select the download mirror closest to your location and click on the link to start the download.

## Splunk Enterprise Download for Linux

1. Go to [Splunk Enterprise Download](https://www.splunk.com/en_us/download/splunk-enterprise.html).
2. Log in to your Splunk account. If you don’t have one, create an account first.
3. Select "Linux" as the platform.
4. Click on "Download Now" for the .tgz file format.
5. On the next page, find the "Download via Command Line (wget)" section.
6. Copy the provided wget command for the Splunk download.

### Using wget to download Splunk Enterprise:

Open a terminal or command prompt:
- Paste the copied wget command:
wget -O splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.1.1/linux/splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz"

- Hit Enter to execute the command.
- This will download the Splunk Enterprise .tgz file to your current directory.

Remember to adjust file names and version numbers if they've been updated since the time of this guide. If you encounter any issues or have further questions, feel free to ask!

## Creating a Virtual Machine

1: Open the Virtual Machine Application
- Launch the Virtual Machine application on your system.

2: Click New Icon
- Locate and click on the "New" or "Create" icon within the application.

3: Setup Name and Operating System
- Name: `<any_name>`
- Choose the operating system as "Microsoft Windows > Linux".

4: Create the VM
- Click "Create".
- Set the File Size to 20GB.

5: Mount ISO file and Configure Network
- Access Settings > Storage > Controller:IDE > Empty.
- Choose the downloaded .iso file for the Optical Drive.
- Access Settings > Storage > Network.
- Change "Attached to" from NAT to Bridge Adapter.

6: Setup & Configure Virtual Machine
- Start the VM or double-click the instance.
- Follow the installation prompts for CentOS 7.
  - Choose 'Install CentOS 7'.
  - Select 'Minimal Install' under Software Selection.
  - Configure installation destination and begin installation.
  - Set the root password.

7: Post-Installation Configuration
- Reboot the VM and log in as root.
- Check network configurations using commands like `ip a`.
- Access network manager using `nmtui`.
  - Edit the connection settings, set hostname, and confirm configurations.

8: Final Checks
- Verify network settings and hostname using commands like `ip a`.
- Quit network manager and perform any additional configurations within the CentOS 7 system.

## SSH into Your Server Using PuTTY

1. **Open PuTTY Application**
   - Launch the PuTTY application on your local system.

2. **Input the Hostname or IP Address**
   - Enter the hostname or IP address of your server in the provided field.

3. **Click Open**
   - Click the "Open" button to initiate the SSH connection.

4. **Login with Your Credentials**
   - When prompted:
     - Username: `root`
     - Enter the password for the root user.

5. **Install 'wget'**
   - After logging in, run the command:
     ```bash
     yum install wget
     ```
   - This command will install the 'wget' utility on your server.

## Create the Splunk Directory and User

1. Create a dedicated user (replace `splunk` with your desired username):

    ```bash
    sudo useradd -m splunk
    ```

2. Set a password for the new user (optional):

    ```bash
    sudo passwd splunk
    ```

3. Create the /opt/splunk directory:

    ```bash
    sudo mkdir /opt/splunk
    ```

4. Set permissions for the directory:

    ```bash
    sudo chown -R splunk:splunk /opt/splunk
    ```

## Installing Splunk Enterprise

1. **Switch to the Splunk User**
   
     ```bash
     sudo su - splunk
     ```
2. **Navigate to the tmp Directory**
    - Change the directory to tmp
    ```bash
    cd /tmp
    ```
    
3. **Download Splunk Enterprise**
   - Run the `wget` command to download Splunk Enterprise:
     ```bash
     wget -O splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.1.1/linux/splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz"
     ```

4. **Untar the Package**
   - Extract the downloaded package:
     ```bash
     tar xvzf splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz -C /opt
     ```

5. **Start and Accept the License**
   - Start Splunk and accept the license agreement:
     ```bash
     /opt/splunk/bin/splunk start --accept-license
     ```
6. **Switch to the Root User**
     ```bash
     su root
     ```
7. **Enable Boot-Start**
   - Enable Splunk to start at boot:
     ```bash
     /opt/splunk/bin/splunk enable boot-start -user splunk
     ```

8. **Enable Port 8000 on Firewall**
   - Add port 8000 to the firewall and reload firewall settings:
     ```bash
     firewall-cmd --permanent --add-port=8000/tcp
     firewall-cmd --reload
     ```
   
9. **Access Splunk Web Interface**
   - Access Splunk's web interface by opening a browser and navigating to `http://your_server_ip:8000`.
   - Log in using the default credentials (username: `admin`, password: `changeme`). It's recommended to change the default password after login.

10. **Configuration and Usage**
   - Further configuration and usage can be done via the Splunk web interface or command line as needed.
