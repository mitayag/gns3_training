# GNS3 Installation Guide: Step-by-Step Procedure

## Prerequisites
- A computer with Windows 10/11, macOS, or Linux
- Administrative privileges on your system
- Minimum 4GB RAM (8GB or more recommended)
- Multi-core processor
- At least 1GB free disk space
- Internet connection for downloading

## Step 1: Download GNS3 Software
1. Visit the official GNS3 website (https://gns3.com/software/download)
2. Create a free account if you don't have one
3. Download the appropriate version for your operating system

## Step 2: Install Required Dependencies
### For Windows:
1. Download and install the latest version of WinPCAP
2. Install Python if not already installed (GNS3 will prompt you)
3. Install Microsoft Visual C++ redistributables if prompted

### For macOS:
1. Install Xcode Command Line Tools:
   ```bash
   xcode-select --install
   ```
2. Install Homebrew (if not installed):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

### For Linux (Ubuntu/Debian):
```bash
sudo apt update
sudo apt install -y python3-pip python3-dev git
sudo apt install -y dynamips ubridge
```

## Step 3: Install GNS3
### Windows Installation:
1. Run the downloaded GNS3 installer
2. Choose "Install GNS3 for all users" (recommended)
3. Accept the license agreement
4. Select components to install:
   - GNS3
   - WinPCAP (if not installed)
   - Npcap (required for packet capture)
   - GNS3 SolarWinds Virtual Machine (optional)
5. Choose installation directory
6. Complete the installation wizard

### macOS Installation:
1. Open the downloaded .dmg file
2. Drag GNS3 to Applications folder
3. Run the following commands:
   ```bash
   brew install gns3
   brew install dynamips
   brew install ubridge
   ```

### Linux Installation:
```bash
sudo add-apt-repository ppa:gns3/ppa
sudo apt update
sudo apt install gns3-gui gns3-server
```

## Step 4: First-Time Setup
1. Launch GNS3
2. The Setup Wizard will appear automatically
3. Choose your setup preference:
   - Local server (recommended for beginners)
   - Remote server (for advanced users)
4. Configure server settings:
   - Keep default local server settings
   - Set host binding (usually 127.0.0.1)
   - Set port number (usually 3080)

## Step 5: Install GNS3 VM (Optional but Recommended)
1. Download VirtualBox or VMware Workstation
2. Download GNS3 VM from the official website
3. Import the VM into your virtualization software:
   - Open VirtualBox/VMware
   - File > Import Appliance
   - Select the downloaded GNS3 VM
   - Accept default settings
   - Start the VM

## Step 6: Verify Installation
1. Open GNS3
2. Create a new project:
   - File > New Project
   - Enter project name
   - Click "OK"
3. Test basic functionality:
   - Add a simple network device
   - Verify server connection status
   - Check console connectivity

## Troubleshooting Common Issues
1. Server Connection Issues:
   - Check if GNS3 server is running
   - Verify firewall settings
   - Confirm port 3080 is not blocked

2. VM Integration Problems:
   - Ensure virtualization is enabled in BIOS
   - Verify VirtualBox/VMware is properly installed
   - Check VM network settings

3. Performance Issues:
   - Adjust memory allocation in preferences
   - Reduce number of simultaneous devices
   - Close unnecessary applications

## Next Steps
1. Download additional device images
2. Configure IOS templates
3. Explore the GNS3 marketplace
4. Join the GNS3 community forum

## Additional Resources
- Official GNS3 Documentation: https://docs.gns3.com/
- GNS3 Community Forums: https://gns3.com/community
- Video Tutorials: https://academy.gns3.com/

Remember to regularly update GNS3 and its components to ensure optimal performance and security.
