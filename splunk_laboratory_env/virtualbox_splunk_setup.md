# Splunk Lab Environment Setup

This guide offers step-by-step instructions for setting up a lab environment using VirtualBox, CentOS, and Splunk Enterprise on a Linux platform.

## Tools Prerequisites

### Oracle VirtualBox Download & Installation

1. Visit the [VirtualBox official website](https://www.virtualbox.org/).
2. Navigate to the "Downloads" section.
3. Choose the appropriate version for your operating system and download the installer.
4. Run the installer and follow the on-screen instructions to install VirtualBox.

### Angry IP Scanner Download & Installation

1. **Visit the Angry IP Scanner official website:**
   Go to [https://angryip.org/download/](https://angryip.org/download/).

2. **Download the Windows installer:**
   - Look for the Windows section on the download page.
   - Download the installer file for the latest version (usually with a .exe extension).

3. **Run the installer:**
   - Locate the downloaded .exe file.
   - Double-click on the file to run the installer.

4. **Follow the installation wizard:**
   - The installation wizard will guide you through the installation process.
   - Choose the installation directory and any additional components you want.

5. **Complete the installation:**
   - Once the installation is complete, you may choose to launch Angry IP Scanner immediately.

6. **Launch Angry IP Scanner:**
   - Find Angry IP Scanner in your Start menu or on your desktop.
   - Double-click on the icon to launch the application.

### MobaXterm Download & Installation

1. **Download MobaXterm:**
   Visit the official MobaXterm website and download the installer: [Download MobaXterm](https://mobaxterm.mobatek.net/).

2. **Run the Installer:**
   Double-click on the downloaded file to run the installer.

3. **Installation Process:**
   Follow the on-screen instructions to install MobaXterm. Customize installation options as needed.

4. **Start MobaXterm:**
   Launch MobaXterm from the Start menu or desktop shortcut.

5. **Optional Registration:**
   If prompted, you can register for a free home edition or continue without registration.

6. **Explore MobaXterm:**
   Open MobaXterm and explore its features, including the terminal, X server, and remote computing tools.

### CentOS Download

1. Visit the [CentOS download page](https://www.centos.org/download/).
2. Choose the CentOS version you want (e.g., CentOS 7 or CentOS 8).
3. Select the download mirror closest to your location and click on the link to start the download.

### Splunk Enterprise Download for Linux

1. Go to [Splunk Enterprise Download](https://www.splunk.com/en_us/download/splunk-enterprise.html).
2. Log in to your Splunk account. If you don’t have one, create an account first.
3. Select "Linux" as the platform.
4. Click on "Download Now" for the .tgz file format.
5. On the next page, find the "Download via Command Line (wget)" section.
6. Copy the provided wget command for the Splunk download.

#### Using wget to download Splunk Enterprise:

Open a terminal or command prompt:
- Paste the copied wget command:
```bash
wget -O splunk-9.1.3-d95b3299fa65-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.1.3/linux/splunk-9.1.3-d95b3299fa65-Linux-x86_64.tgz"
```
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

## Using MobaXterm to SSH into a Server

1. Launch MobaXterm
   - Open MobaXterm from the Start menu or desktop shortcut.

2. Open the "Session" Pane
   - In the MobaXterm interface, find the menu bar at the top.
   - Click on the "Session" button.

3. Choose SSH as the Session Type
   - In the "Session" pane, select the "SSH" tab on the left.

4. Enter Server Information
   - Under "Basic SSH settings," provide the following information:
      - **Remote Host:** Enter the IP address or hostname of the server.
      - **Specify username:** Input your username on the remote server.

5. Click "OK" to Connect
   - Once the information is entered, click the "OK" button at the bottom of the "Session" pane.

6. Enter Password (if applicable)
   - If it's your first time connecting or if password authentication is required, MobaXterm will prompt you for your password.
   - Type your password and press Enter.

7. Successful Connection
   - If configured correctly, you should now be connected to the remote server.
   - The terminal window within MobaXterm will display the command line of the remote server.

8. Install 'wget'
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
     wget -O splunk-9.1.3-d95b3299fa65-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.1.3/linux/splunk-9.1.3-d95b3299fa65-Linux-x86_64.tgz"
     ```

4. **Untar the Package**
   - Extract the downloaded package:
     ```bash
     tar xvzf splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz -C /opt
     ```

4. **Start and Accept the License**
   - Start Splunk and accept the license agreement:
     ```bash
     /opt/splunk/bin/splunk start --accept-license
     ```
5. **Switch to the Root User**
     ```bash
     su root
     ```
6. **Enable Boot-Start**
   - Enable Splunk to start at boot:
     ```bash
     /opt/splunk/bin/splunk enable boot-start -user splunk
     ```

7. **Enable Port 8000 on Firewall**
   - Add port 8000 to the firewall and reload firewall settings:
     ```bash
     firewall-cmd --zone=public --add-port=8000/tcp --permanent
     firewall-cmd --reload
     ```
   
8. **Access Splunk Web Interface**
   - Access Splunk's web interface by opening a browser and navigating to `http://your_server_ip:8000`.
   - Log in using the default credentials (username: `admin`, password: `changeme`). It's recommended to change the default password after login.

9. **Configuration and Usage**
   - Further configuration and usage can be done via the Splunk web interface or command line as needed.
