# Hands-on Guide: Creating a GNS3 Project and Loading IOS Images

## Prerequisites
- GNS3 installed and running
- GNS3 VM configured (if using VM-based setup)
- Cisco IOS image file (.bin or .image format)
- Sufficient system resources

## Part 1: Creating a New Project

### Step 1: Launch GNS3
1. Open GNS3 application
2. Wait for the server to initialize (check status in bottom right)

### Step 2: Create New Project
1. Click File > New Project
2. In the New Project dialog:
   - Enter project name (e.g., "First_Network")
   - Choose project location
   - Select "Open in new workspace"
   - Click "OK"

### Step 3: Save Project
1. Click File > Save
2. Verify project appears in recent projects list

## Part 2: Loading IOS Images

### Step 1: Access IOS Image Configuration
1. Go to Edit > Preferences
2. Navigate to "IOS Routers" section
3. Click "New" to add a new IOS image

### Step 2: Configure New IOS Router Template
1. In the "New IOS router template" wizard:
   ```
   Step 1: Select platform
   - Choose router platform (e.g., c7200)
   - Click "Next"

   Step 2: Select IOS image
   - Click "Browse"
   - Navigate to your IOS image file
   - Select the file
   - Click "Next"

   Step 3: Memory settings
   - RAM: Set as per image requirements (default 512 MB)
   - NVRAM: Keep default (usually 128 KB)
   - Click "Next"

   Step 4: Network adapters
   - Select required adapters
   - Common choices: FastEthernet, GigabitEthernet
   - Click "Next"

   Step 5: Idle-PC finder
   - Click "Idle-PC finder"
   - Wait for calculation
   - Select recommended value
   - Click "Next"

   Step 6: Summary
   - Review settings
   - Click "Finish"
   ```

### Step 3: Verify IOS Image Installation
1. Check IOS Routers section in Preferences
2. Verify new template appears in list
3. Ensure status shows as "Ready"

## Part 3: Creating Router Instance

### Step 1: Add Router to Workspace
1. Drag router from Devices panel to workspace
2. Wait for initialization

### Step 2: Configure Basic Settings
1. Right-click router > Configure
2. Verify settings:
   ```
   - Name
   - Platform
   - Image version
   - RAM allocation
   - Network adapters
   ```

## Part 4: Common Issues and Troubleshooting

### Image Loading Issues
1. Checksum verification failed:
   - Verify image file integrity
   - Re-download if necessary
   - Check MD5/SHA sum if available

2. Insufficient memory:
   ```
   Solutions:
   - Increase RAM allocation
   - Close unnecessary applications
   - Check GNS3 VM resources
   ```

3. Image incompatibility:
   - Verify image supports chosen platform
   - Check GNS3 compatibility list

### Idle-PC Value Problems
1. High CPU usage:
   - Recalculate Idle-PC value
   - Try different suggested values
   - Ensure virtualization is enabled

2. Router doesn't boot:
   ```
   Steps:
   1. Delete Idle-PC value
   2. Restart router
   3. Recalculate value
   ```

## Part 5: Best Practices

### Project Organization
1. Use meaningful project names
2. Create project folders structure:
   ```
   ProjectName/
   ├── configs/
   ├── images/
   └── documentation/
   ```

### IOS Image Management
1. Maintain image inventory:
   ```
   - Image version
   - Platform compatibility
   - Memory requirements
   - Idle-PC values
   ```

2. Regular backups:
   - Save working configurations
   - Document successful settings

### Performance Optimization
1. Resource allocation:
   ```
   - Allocate appropriate RAM
   - Monitor CPU usage
   - Balance device count
   ```

2. Regular maintenance:
   - Clear unused projects
   - Remove unused images
   - Update GNS3 regularly

## Verification Checklist
- [ ] Project creates successfully
- [ ] IOS image loads without errors
- [ ] Router boots properly
- [ ] Idle-PC value is set
- [ ] CPU usage is normal
- [ ] Basic configuration possible
- [ ] Settings are saved

## Additional Tips
1. Keep original IOS images backed up
2. Document working Idle-PC values
3. Test configurations before large deployments
4. Use consistent naming conventions
5. Regularly save project progress

## Next Steps
1. Basic router configuration
2. Network topology design
3. Adding more devices
4. Testing connectivity
