# OPcache Auto Configuration Script

## Overview
This script automates the detection of installed PHP versions on a server and configures **OPcache** settings based on server resources (RAM and CPU) and workload type (Shared Hosting, High-Traffic Website, or E-commerce). The script also applies changes to the respective configuration files and restarts the web server to activate the new settings.

## Features
- **Dynamic Resource-Based Configuration**: Automatically adjusts OPcache memory and settings based on server RAM and the selected workload type.
- **Support for Multiple PHP Versions**: Detects and applies configurations to all installed PHP versions.
- **Admin Prompt**: Asks the admin to specify the server's workload type for optimized settings.
- **Web Server Restart**: Restarts LiteSpeed or Apache after applying the configuration.

## Supported Environments
- **Operating Systems**: Linux-based systems (e.g., CentOS, AlmaLinux, CloudLinux).
- **Web Servers**: LiteSpeed, Apache.
- **PHP Management**: Supports PHP installations managed by cPanel and CloudLinux.

## Workload Types
1. **Shared Hosting**:
   - Optimized for multi-tenant environments.
   - Lower memory usage and higher revalidation frequency.

2. **High-Traffic Website**:
   - Optimized for websites with high concurrent users.
   - Increased OPcache memory and lower revalidation frequency.

3. **E-commerce**:
   - Designed for performance-critical e-commerce platforms.
   - Maximum memory allocation and zero revalidation frequency for stability.

## How to Use
1. **Download the Script**:
   Save the script as `opcache_auto_config.sh`.

2. **Make the Script Executable**:
   ```bash
   chmod +x opcache_auto_config.sh
   ```

3. **Run the Script**:
   Execute the script with root privileges:
   ```bash
   sudo ./opcache_auto_config.sh
   ```

4. **Follow the Prompts**:
   - Select the server workload type (Shared Hosting, High-Traffic Website, or E-commerce).
   - The script will automatically configure OPcache for all detected PHP versions.

5. **Verify the Configuration**:
   - Check the OPcache settings by running:
     ```bash
     php -i | grep opcache
     ```
   - Verify the web server is running:
     ```bash
     systemctl status lsws
     ```
     or
     ```bash
     systemctl status httpd
     ```

## OPcache Configuration
The script applies the following settings dynamically based on server resources and workload type:

| Setting                     | Shared Hosting | High-Traffic Website | E-commerce |
|-----------------------------|----------------|-----------------------|------------|
| `opcache.memory_consumption` | 128 MB         | 128-512 MB           | 128-512 MB |
| `opcache.max_accelerated_files` | 10,000         | 20,000               | 30,000     |
| `opcache.revalidate_freq`   | 60 seconds     | 1 second             | 0 seconds  |

## Logs
The script logs OPcache-related errors and messages to `/var/log/opcache.log`.

## Troubleshooting
- **Permission Errors**: Ensure the script has write access to PHP configuration files.
- **Web Server Not Restarting**: Restart the server manually if the script fails to detect it.
- **Invalid Workload Type**: Enter a valid option (1, 2, or 3) when prompted.

## Contributions
Feel free to contribute by suggesting improvements or submitting pull requests. This project aims to simplify and optimize OPcache configuration for diverse workloads.


