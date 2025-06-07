# Flux Toolkit

A specialized collection of monitoring and maintenance scripts designed to enhance the stability and reliability of Flux network nodes. This toolkit provides automated solutions for database monitoring, benchmark validation, and system updates to ensure optimal node performance.

## 📋 Table of Contents

1. [Features](#-features)
2. [Database Health Monitor (checkdb.sh)](#-database-health-monitor-checkdbsh)
3. [Benchmark Validation Monitor (benchcheck.sh)](#-benchmark-validation-monitor-benchchecksh)
4. [Automated System Updates (autoupdate_system.sh)](#-automated-system-updates-autoupdate_systemsh)
5. [Crontab Management](#-crontab-management)
6. [Quick Start Guide](#-quick-start-guide)
7. [Important Notes](#️-important-notes)
8. [Contributing](#-contributing)
9. [License](#-license)

## 🚀 Features

- **Database Monitoring**: Automated database health checks with automatic recovery
- **Benchmark Validation**: Continuous monitoring of FluxBench status with auto-correction
- **System Maintenance**: Intelligent system updates with maintenance window awareness
- **Automated Recovery**: Self-healing mechanisms to maintain node uptime
- **Production-Ready**: Battle-tested scripts for reliable node operation

---

## 🔍 Database Health Monitor (checkdb.sh)

This critical monitoring script ensures your Flux node's database remains operational by performing regular health checks and automatically recovering from database failures.

**Key Features:**
- Monitors database status every 10 minutes
- Automatically reboots the host if database is unresponsive
- Prevents extended downtime from database crashes
- Minimal resource overhead
- Reliable failsafe mechanism

**Installation and Setup:**
```
wget https://raw.githubusercontent.com/en4ble1337/flux-repository/main/checkdb.sh && chmod 777 checkdb.sh && (crontab -l ; echo "*/10 *  */home/$USER/checkdb.sh") | crontab -
```

**What it does:**
- Runs every 10 minutes via crontab
- Checks if the Flux database is responding
- Initiates system reboot if database is unresponsive
- Logs activity for troubleshooting purposes

---

## 🎯 Benchmark Validation Monitor (benchcheck.sh)

This high-frequency monitoring script ensures your node's benchmark status remains valid by detecting FluxBench failures and automatically triggering re-benchmarking when needed.

**Key Features:**
- Monitors FluxBench status every minute
- Detects benchmark failures instantly
- Automatically forces re-benchmarking
- Maintains node eligibility for rewards
- Prevents manual intervention requirements

**Installation and Setup:**
```
wget https://raw.githubusercontent.com/en4ble1337/flux-repository/main/benchcheck.sh && chmod 777 benchcheck.sh && (crontab -l ; echo "* *  */home/$USER/benchcheck.sh") | crontab -
```

**What it does:**
- Executes every minute for rapid failure detection
- Monitors FluxBench process status
- Automatically initiates re-benchmarking on failure
- Ensures continuous node qualification

---

## 🔄 Automated System Updates (autoupdate_system.sh)

An intelligent update management system that keeps your Flux node current while respecting operational windows and node status. This script provides hands-off maintenance for production environments.

**Advanced Features:**
- Automatic OS and FluxOS updates
- Maintenance window awareness
- Queue status detection
- Intelligent reboot postponement
- Comprehensive logging
- Zero-downtime update strategy

**Important Prerequisites:**
- **Do not run Flux watchdog** for proper operation
- Ensure maintenance windows are properly configured
- Verify queue detection is working correctly

**Installation and Setup:**
```
wget https://raw.githubusercontent.com/mike8643/fluxnode---system-auto-update/main/autoupdate_system.sh && chmod +x autoupdate_system.sh && mkdir crontab_logs && touch crontab_logs/autouptade_os.log && crontab -l | sed "\$a0 23 * ** /home/$USER/autoupdate_system.sh >> /home/$USER/crontab_logs/autouptade_os.log 2>&1" | crontab -
```

**Script Behavior:**
- Runs daily at 23:00 (11 PM)
- Updates system packages and FluxOS
- Checks node status before rebooting
- Postpones reboots during active periods
- Logs all activities to `crontab_logs/autouptade_os.log`

**Credits:**
Full credit to [mike8643](https://github.com/mike8643/fluxnode---system-auto-update) for the original implementation.

---

## 🛠️ Crontab Management

Proper crontab management is essential for maintaining your automated scripts. Use these commands to manage your scheduled tasks effectively.

**Remove a specific crontab entry (example with checkdb.sh):**
```
crontab -l | grep -v "/home/fluxadmin/checkdb.sh" | crontab -
```

**View all current crontabs:**
```
crontab -l
```

**Edit crontabs manually:**
```
crontab -e
```

**Common Crontab Patterns:**
- `*/10 * * * *` - Every 10 minutes
- `* * * * *` - Every minute  
- `0 23 * * *` - Daily at 11 PM
- `0 */6 * * *` - Every 6 hours

---

## 🚀 Quick Start Guide

### For New Node Setup:
1. **Install Database Monitor**: Set up checkdb.sh for database reliability
2. **Install Benchmark Monitor**: Deploy benchcheck.sh for benchmark validation
3. **Configure Auto-Updates**: Implement autoupdate_system.sh for maintenance
4. **Verify Crontabs**: Check all scheduled tasks are running properly

### For Existing Nodes:
1. **Backup Current Crontabs**: `crontab -l > crontab_backup.txt`
2. **Install Required Scripts**: Follow individual installation commands
3. **Test Script Execution**: Manually run scripts to verify functionality
4. **Monitor Logs**: Check log files for proper operation

---

## ⚠️ Important Notes

**Critical Considerations:**
- **Disable Flux watchdog** when using autoupdate_system.sh to prevent conflicts
- **Test in development** environment before deploying to production nodes
- **Monitor log files** regularly to ensure scripts are functioning correctly
- **Backup crontabs** before making changes
- **Verify script permissions** (chmod 777) are applied correctly

**Security Considerations:**
- Scripts run with user privileges - ensure proper file permissions
- Log files may contain sensitive information - secure appropriately
- Regular security updates are handled by autoupdate_system.sh

**Performance Impact:**
- Database checks every 10 minutes have minimal resource impact
- Benchmark checks every minute are lightweight operations
- System updates run daily during off-peak hours

---

## 📊 Monitoring and Troubleshooting

**Log File Locations:**
- Auto-update logs: `~/crontab_logs/autouptade_os.log`
- System logs: `/var/log/syslog`
- Crontab logs: Check individual script output

**Common Issues:**
- **Scripts not executing**: Check file permissions and crontab syntax
- **Database false positives**: Verify database connection parameters
- **Update conflicts**: Ensure Flux watchdog is disabled
- **Permission errors**: Verify user has necessary system privileges

---

## 🤝 Contributing

We welcome contributions to improve the Flux Toolkit! Whether you're fixing bugs, adding features, or improving documentation, your help is appreciated.

**How to Contribute:**
- Fork the repository
- Create a feature branch
- Test your changes thoroughly
- Submit a pull request with detailed description

---

## 📄 License

This project is open source and available under standard open source licensing terms. Individual scripts may have their own licensing - please check script headers for specific details.
