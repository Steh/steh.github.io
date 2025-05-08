---
title: "MacOS Forensics"
categories: 
  - informationsecurity
tags:
  - blue team
classes: 
  - wide
excerpt: ""
toc: true
--- 

# macOS File Types and Their Locations

## .plist Files (Property List Files)

- **Purpose**: Store system and application configurations, similar to the Windows Registry.
- **Formats**: XML or Binary (BLOB).
- **Common Locations**:
  - System-wide settings: `/Library/Preferences/`
  - User-specific settings: `~/Library/Preferences/`
  - Application-specific settings: Inside `.app` bundles or `~/Library/Application Support/`
- **Forensic Importance**: Contain user settings, application preferences, and system configurations.
- **Tools for Analysis**:
  - macOS: Xcode, `plutil`, Plist Editor Pro.
  - Cross-platform: `plistutil`, Python libraries like `biplist` or `plistlib`.

## .app Files

- **Purpose**: Executable application bundles for macOS.
- **Structure**: Bundles often contain the executable, resources, and metadata.
- **Common Locations**:
  - **System-wide applications**: `/Applications/`
  - **User-specific applications**: `~/Applications/`
  - **System utilities**: `/System/Applications/`
- **Forensic Importance**: Application metadata and logs within the bundle may provide insights into user activity, timestamps, or potential malware behavior.
- **How to Inspect**: Right-click the `.app` file and select **Show Package Contents**.

## .dmg Files

- **Purpose**: Disk image files used for software distribution or backups.
- **File Systems**: APFS, HFS+, or FAT.
- **Common Locations**:
  - Downloaded installers: `~/Downloads/`
  - Mounted disk images: `/Volumes/<disk_name>/`
- **Forensic Importance**:
  - Mounted `.dmg` files can reveal software installers, file structures, or hidden files.
  - Analyze `.dmg` files for malicious payloads or unauthorized software.
- **Tools for Analysis**:
  - macOS: Disk Utility, `hdiutil`.
  - Cross-platform: `7-Zip`, forensic tools like Autopsy.

## .kext Files (Kernel Extensions)

- **Purpose**: Kernel-level modules, akin to drivers in Windows.
- **Current Status**: Deprecated in macOS Big Sur and later.
- **Common Locations**:
  - `/System/Library/Extensions/`
  - `/Library/Extensions/`
- **Forensic Importance**:
  - Older macOS versions: Investigate `.kext` files for unauthorized kernel modifications or malware.
  - Newer macOS versions: Look for traces of attempts to bypass the stricter security model.
- **Tools for Analysis**: Use `kextstat` to list loaded kernel extensions and inspect their origins.

## .dylib Files (Dynamic Libraries)

- **Purpose**: Shared libraries, similar to `.dll` files in Windows or `.so` files in Linux.
- **Common Locations**:
  - System libraries: `/usr/lib/`
  - Application-specific libraries: Inside `.app` bundles or `/Library/Frameworks/`
- **Forensic Importance**:
  - Analyze for signs of malicious code injection or unauthorized library usage.
  - Check for persistence mechanisms that use malicious `.dylib` files.
- **Tools for Analysis**:
  - Use `otool` or `dyldinfo` on macOS to inspect dependencies.
  - Cross-reference with known good libraries to identify anomalies.

## .xar Files (eXtensible ARchive)

- **Purpose**: Archive format often used for macOS installers or browser extensions.
- **Common Locations**:
  - Installer packages: `/private/var/tmp/` (temporary location during installation).
  - Browser extensions: `~/Library/Application Support/<browser_name>/Extensions/`
- **Forensic Importance**:
  - Inspect for malicious payloads or tampered installers.
  - Analyze metadata for timestamps and source information.
- **Tools for Analysis**:
  - Use `xar` (command-line tool) or `7-Zip` to extract and analyze contents.

# Mounting APFS Disk Image

You can use `apfs-fuse` to mount APFS disk images for analysis or troubleshooting.

## Prerequisites

- Install **apfs-fuse** and **FUSE** (required for user-space file systems).

```bash
# install the required dependencies
sudo apt update
sudo apt install cmake libfuse-dev libicu-dev g++ git

# Clone the apfs-fuse repository from GitHub
git clone https://github.com/sgan81/apfs-fuse.git
cd apfs-fuse

# build the tools
mkdir build
cd build
cmake ..
make

# install binaries
sudo make install

# verify
apfsutil --help
apfs-fuse --help
```

## Steps

1. **List Volumes in the APFS Container**  

Run the following command to inspect the disk image:

```bash
apfsutil mac-disk.img
```

2. **Mount the Disk Image**

Mount the image to a directory (e.g., `mac/`):
```bash

apfs-fuse mac-disk.img mac/

# mount the 4 volume
apfs-fuse -v 4 mac-disk.img mac
```

## Resources

- [apfs-fuse GitHub](https://github.com/sgan81/apfs-fuse)  
- [FUSE Documentation](https://github.com/libfuse/libfuse)

# macOS Forensic Artefacts Overview

macOS forensic artefacts can be categorized into a few key types, each requiring specific tools or parsers to extract and analyze data. Below is an overview of the most common artefacts and the tools used to handle them.

---

## **Plist Files**

Plist (Property List) files are a common artefact type in macOS, storing configuration and application data. They can be in **XML** or **BLOB** format:
- **XML**: Readable using built-in utilities like `cat`, `more`, or `head`.
- **BLOB**: Requires specific utilities to parse.

### **Tools for Plist Files**

- **macOS**: Use `plutil` to parse BLOB plist files:
  ```bash
  plutil -p <file>.plist
  ```
- **Linux**: Use `plistutil` (similar to `plutil`):
  ```bash
  plistutil -p <file>.plist
  ```

---

## **Database Files**

macOS stores artefacts like chat history, browsing history, and app usage in SQLite databases.

### **Tools for Database Files**

- **DB Browser for SQLite**: A cross-platform GUI tool for exploring SQLite databases.
- **APOLLO**: A framework to extract and parse macOS databases, creating timelines and reports.

### **Example Commands**

- Start **DB Browser** (on the attached VM):
  ```
  Applications > Accessories > DB Browser for SQLite
  ```
- Run APOLLO to extract and parse data:
  ```bash
  python3 apollo.py extract -osql_json -pyolo -vyolo modules tmp_apollo
  ```

---

## **Logs**

macOS logs provide a wealth of forensic information. They are categorized into three main types:

### **Apple System Logs (ASL)**

- **Location**: `/private/var/log/asl/`
- **Tools**:
  - **macOS**: Use the Console app:
    ```bash
    open -a Console /private/var/log/asl/<log>.asl
    ```
  - **Linux/Windows**: Use `mac_apt` to parse ASL logs:
    ```bash
    python3 mac_apt.py -o output_path input_type input_path ASL
    ```

### **System Logs**

- **Location**: `/private/var/log/system.log`
- **Notes**: Logs are rotated into `.gz` files. Use `zgrep` to search compressed logs:
  ```bash
  zgrep BOOT_TIME system.log*
  ```

### **Unified Logs**

- **Location**: `/private/var/db/diagnostics/*.tracev3` and `/private/var/db/uuidtext`
- **Tools**:
  - **macOS**: Use the `log` command:
    ```bash
    log show --last 1m
    ```
  - **Unified Log Parser**: Convert logs to CSV/JSON for analysis:
    ```bash
    ./unifiedlog_parser -i <logarchive> -o <output_file>
    ```

---

## **Key Tools Summary**

| Artefact Type     | Tool                     | Platform       | Command/Usage Example                     |
|-------------------|--------------------------|----------------|-------------------------------------------|
| **Plist Files**   | `plutil` / `plistutil`   | macOS/Linux    | `plutil -p <file>.plist`                  |
| **Databases**     | DB Browser, APOLLO       | Cross-platform | `python3 apollo.py extract ...`           |
| **ASL Logs**      | `mac_apt`                | Cross-platform | `python3 mac_apt.py ...`                  |
| **System Logs**   | `zgrep`                  | macOS/Linux    | `zgrep BOOT_TIME system.log*`             |
| **Unified Logs**  | Unified Log Parser       | Cross-platform | `./unifiedlog_parser -i <logarchive>`     |

---

This concise overview provides a quick reference for handling macOS forensic artefacts and the tools required for analysis. Let me know if you'd like further refinements!

# Verifying System Information in macOS Forensics

When performing forensics, verifying system information is essential to ensure we are analyzing the correct system. Below is an overview of key artefacts and methods to retrieve system-related data.

---

## **OS Version**

The macOS version is stored in a plist file located at:
```
/System/Library/CoreServices/SystemVersion.plist
```

### **Example Command**

```bash
cat /System/Library/CoreServices/SystemVersion.plist
```
- **Note**: Use `plutil` to read plist files in binary format:
  ```bash
  plutil -p <file>.plist
  ```

---

## **Serial Number**

The serial number is not stored directly on disk but can be retrieved from:
- **Crash Reports**: `/System/Volumes/Data/Library/Logs/CrashReporter`
- **Spotlight Metadata**: `/System/Volumes/Data/.Spotlight-V100`

### **Live System Commands**

1. Using `system_profiler`:
   ```bash
   system_profiler SPHardwareDataType | awk '/Serial/ {print $4}'
   ```
2. Using `ioreg`:
   ```bash
   ioreg -rd1 -c IOPlatformExpertDevice | awk -F '"' '/IOPlatformSerialNumber/ {print $4}'
   ```

---

## **OS Installation and Update Dates**

### **Method 1: Using `.AppleSetupDone**

The file `/private/var/db/.AppleSetupDone` contains timestamps:
- **Command**:
  ```bash
  stat -x /private/var/db/.AppleSetupDone
  ```

### **Method 2: Using `journal.plist`

Detailed installation and update history can be found in:
```
/private/var/db/softwareupdate/journal.plist
```

### **Example Command**

```bash
cat /private/var/db/softwareupdate/journal.plist
```

---

## **Time Zone**

### **Current Time Zone**

The `/etc/localtime` file contains the current time zone:
```bash
ls -la /etc/localtime
```

### **Time Zone History**

Historical time zones are stored in:
```
/Library/Preferences/.GlobalPreferences.plist
```

### **Example Command**

```bash
plutil -p /Library/Preferences/.GlobalPreferences.plist
```

### **Auto Time Zone Configuration**

Check if time zone auto-adjustment is active:
```bash
plutil -p /Library/Preferences/com.apple.timezone.auto.plist
```

---

## **Boot, Reboot, and Shutdown Times**

### **System Logs**

Boot and shutdown times can be found in:
```
/private/var/log/system.log
```
- **Search Commands**:
  ```bash
  zgrep BOOT_TIME system.log.*
  zgrep SHUTDOWN_TIME system.log.*
  ```

### **Unified Logs**

Unified logs provide more details, including screen lock and unlock events:
- **Command to Filter Shutdown Events**:
  ```bash
  log show --info --predicate 'eventMessage contains "com.apple.system.loginwindow" and eventMessage contains "SessionAgentNotificationCenter"'
  ```

---

This overview provides a quick reference for retrieving critical system information during macOS forensic investigations. Let me know if you'd like to refine or expand this further!

# Identifying macOS Network Configuration

When performing macOS forensics, analyzing a machine's network configuration can reveal critical information about its interfaces, DHCP settings, wireless connections, and network usage.

---

## **Network Interfaces**

The network interfaces of a macOS machine are stored in:
```
/Library/Preferences/SystemConfiguration/NetworkInterfaces.plist
```

### **Example Command**

```bash
cat /Library/Preferences/SystemConfiguration/NetworkInterfaces.plist
```

Each interface is enclosed in a `<dict>` tag. Key attributes include:
- **SCNetworkInterfaceType**: Identifies the interface type (e.g., `IEEE80211` for Wi-Fi, `Ethernet` for wired networks).
- **BSD Name**: The interface name (e.g., `en0`, `en1`).

---

## **DHCP Settings**

DHCP settings for specific interfaces (e.g., `en0`) are stored in:
```
/private/var/db/dhcpclient/leases/<interface>.plist
```

### **Example Command**

```bash
sudo cat /private/var/db/dhcpclient/leases/en0.plist
```

Key attributes include:
- **IPAddress**: Assigned IP address.
- **RouterIPAddress**: Gateway address.
- **SSID**: Network name.
- **LeaseStartDate**: Start date of the DHCP lease.
- **LeaseLength**: Duration of the lease.

---

## **Wireless Connections**

Historical wireless connections are stored in:
```
/Library/Preferences/com.apple.wifi.known-networks.plist
```

### **Example Command**

```bash
sudo plutil -p /Library/Preferences/com.apple.wifi.known-networks.plist
```

Key details include:
- **SSID**: Network name.
- **AddedAt**: Date when the network was added.
- **LastAssociatedAt**: Last connection date.
- **SupportedSecurityTypes**: Network security type (e.g., WPA/WPA2).
- **Location Coordinates**: Latitude and longitude of access points (if available).

---

## **Network Usage**

Unified logs provide information about network connections and changes. On a live system, search for logs using:
```bash
log show --info --predicate 'senderImagePath contains "IPConfiguration" and (eventMessage contains "SSID" or eventMessage contains "Lease" or eventMessage contains "network changed")'
```

### **Example Output**

- **SSID**: Network name.
- **NetworkID**: Unique identifier for the network.
- **Security**: Encryption type (e.g., FT_PSK).

### **Offline Analysis**

If the system is not live, convert unified logs to CSV for analysis:
```bash
./unifiedlog_parser -i system_logs.logarchive -o logs/output.csv
```
- Search for keywords like `IPConfiguration`, `SSID`, or `network changed` in the resulting CSV file.
https://cloud.google.com/blog/topics/threat-intelligence/reviewing-macos-unified-logs/?hl=en

## Sources

* [TryHackMe - macOS Forensics Basics](https://tryhackme.com/room/macosforensicsbasics)
* [TryHackMe - macOS Forensics Artefacts](https://tryhackme.com/room/macosforensicsartefacts)
* [GitHub - mac4n6](https://github.com/pstirparo/mac4n6)
* [Cloud Google Blog - Reviewing macOS Unified Logs](https://cloud.google.com/blog/topics/threat-intelligence/reviewing-macos-unified-logs/?hl=en)