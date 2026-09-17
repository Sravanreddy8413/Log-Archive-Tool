https://roadmap.sh/projects/log-archive-tool

# 📦 Log Archive Tool

A beginner-friendly **Linux Bash/Shell Scripting project** that provides a simple command-line tool for archiving log files.

The tool accepts a log directory as an argument, compresses the logs into a `.tar.gz` archive, stores the archive in a dedicated directory, and records the archive date and time in a log file.

---

## 📌 Project Overview

Linux servers continuously generate log files from services such as:

* Nginx
* Apache
* SSH
* Docker
* Systemd
* Applications
* Databases

Over time, log files can consume significant disk space.

Instead of deleting old logs permanently, this project provides a simple way to **compress and archive logs** for future reference.

The most common Linux log directory is:

```text
/var/log
```

---

## 🎯 Project Goal

Build a command-line tool:

```bash
log-archive <log-directory>
```

that can:

1. Accept a log directory as an argument.
2. Validate that the directory exists.
3. Create an archive directory.
4. Compress the specified logs into `.tar.gz`.
5. Generate a timestamped archive filename.
6. Store the archive in the archive directory.
7. Record the archive date and time.
8. Display useful status messages.

---

# 🚀 Features

* ✅ Command-line interface
* ✅ Accepts log directory as an argument
* ✅ Validates input
* ✅ Creates archive directory automatically
* ✅ Compresses logs using `tar`
* ✅ Generates timestamped archive names
* ✅ Stores archives separately from source logs
* ✅ Maintains archive history
* ✅ Records archive date and time
* ✅ Error handling
* ✅ Exit status handling

---

# 🏗️ Project Structure

```text
log-archive-tool/
│
├── log-archive
│
├── archives/
│
├── archive.log
│
└── README.md
```

After running the tool:

```text
log-archive-tool/
│
├── log-archive
├── archives/
│   ├── logs_archive_20260917_101530.tar.gz
│   ├── logs_archive_20260918_091245.tar.gz
│   └── logs_archive_20260919_114512.tar.gz
│
├── archive.log
└── README.md
```

---

# 🛠️ Technologies Used

| Technology | Purpose                    |
| ---------- | -------------------------- |
| Linux      | Operating system           |
| Bash       | Scripting language         |
| `tar`      | Compress and archive logs  |
| `date`     | Generate timestamps        |
| `mkdir`    | Create directories         |
| `ls`       | List files                 |
| `find`     | Locate files               |
| `test`     | Validate files/directories |
| CLI        | Command-line interface     |

---

# 📋 Requirements

You need:

* Linux
* Bash
* `tar`
* Standard Unix/Linux utilities

Check Bash:

```bash
bash --version
```

Check `tar`:

```bash
tar --version
```

---

# 📥 Installation

## 1. Clone the Repository

```bash
git clone https://github.com/<YOUR-USERNAME>/log-archive-tool.git
```

Move into the project:

```bash
cd log-archive-tool
```

---

## 2. Check Files

```bash
ls -la
```

Expected:

```text
README.md
log-archive
```

---

## 3. Make the Tool Executable

```bash
chmod +x log-archive
```

Verify:

```bash
ls -l log-archive
```

Expected permissions:

```text
-rwxr-xr-x
```

---

# ▶️ Usage

The basic syntax is:

```bash
./log-archive <log-directory>
```

For example:

```bash
./log-archive /var/log
```

If you are archiving a directory owned by root, you may need:

```bash
sudo ./log-archive /var/log
```

---

# 📦 Archive Naming Convention

The archive filename follows this format:

```text
logs_archive_YYYYMMDD_HHMMSS.tar.gz
```

Example:

```text
logs_archive_20260917_101530.tar.gz
```

Where:

```text
2026 → Year
09   → Month
17   → Day
10   → Hour
15   → Minute
30   → Second
```

This makes each archive easy to identify.

---

# 🗜️ How `tar` Works

The project uses:

```bash
tar -czf
```

Example:

```bash
tar -czf logs_archive_20260917_101530.tar.gz /var/log
```

Options:

| Option | Meaning                  |
| ------ | ------------------------ |
| `c`    | Create archive           |
| `z`    | Compress using gzip      |
| `f`    | Specify archive filename |

The resulting file has:

```text
.tar.gz
```

extension.

---

# 📂 Archive Directory

The tool creates an archive directory if it doesn't already exist.

Example:

```text
archives/
```

Archives are stored there:

```text
archives/logs_archive_20260917_101530.tar.gz
```

This keeps archived logs separate from active logs.

---

# 📝 Archive Log

The tool records archive activity in:

```text
archive.log
```

Example:

```text
2026-09-17 10:15:30 - Archived /var/log
2026-09-18 09:12:45 - Archived /var/log/nginx
2026-09-19 11:45:12 - Archived /var/log/apache2
```

This provides a simple history of when archives were created.

---

# 🔍 Example Workflow

### Step 1 — Check the log directory

```bash
ls -lh /var/log
```

Example:

```text
auth.log
syslog
kern.log
nginx/
```

---

### Step 2 — Run the archive tool

```bash
./log-archive /var/log
```

---

### Step 3 — Check the archive directory

```bash
ls -lh archives/
```

Example:

```text
logs_archive_20260917_101530.tar.gz
```

---

### Step 4 — Check archive log

```bash
cat archive.log
```

Example:

```text
2026-09-17 10:15:30 - Archived /var/log successfully
```

---

# 🔎 Verify the Archive

You can inspect the contents without extracting:

```bash
tar -tzf archives/logs_archive_20260917_101530.tar.gz
```

Example:

```text
var/log/
var/log/syslog
var/log/auth.log
var/log/kern.log
```

---

# 📤 Extract an Archive

Create a directory:

```bash
mkdir extracted-logs
```

Extract:

```bash
tar -xzf archives/logs_archive_20260917_101530.tar.gz -C extracted-logs
```

Check:

```bash
ls -R extracted-logs
```

---

# 🧪 Testing

Check Bash syntax:

```bash
bash -n log-archive
```

A successful syntax check produces no output.

You can also run:

```bash
bash -x log-archive /var/log
```

The `-x` option displays the commands executed by the script and is useful for troubleshooting.

---

# ❌ Error Handling

The tool should handle common errors.

### No argument

```bash
./log-archive
```

Expected:

```text
Usage: ./log-archive <log-directory>
```

---

### Directory doesn't exist

```bash
./log-archive /invalid/log/path
```

Expected:

```text
Error: Log directory does not exist.
```

---

### Permission issue

If the user does not have permission to read the log directory:

```text
Error: Permission denied.
```

For system logs, run:

```bash
sudo ./log-archive /var/log
```

when appropriate.

---

# 🔐 Linux Permissions

Linux log files can contain sensitive system information.

Check permissions:

```bash
ls -ld /var/log
```

Check individual log files:

```bash
ls -l /var/log
```

Do not make sensitive log archives world-readable.

For example, avoid unnecessarily using:

```bash
chmod 777 archives/
```

Instead, use appropriate ownership and permissions.

---

# 💡 Why Log Archiving Is Important

Production servers generate logs continuously.

For example:

```text
Application
     |
     v
Log Files
     |
     v
Disk Usage Increases
     |
     v
Disk Almost Full
     |
     v
Application Problems
```

Log archiving provides:

```text
Active Logs
     |
     v
Archive
     |
     v
Compress
     |
     v
Store
     |
     v
Remove/rotate old active logs
```

This helps maintain disk capacity while preserving historical logs.

> In production environments, log rotation and centralized logging systems are normally preferred over manually archiving the entire `/var/log` directory.

---

# ⏰ Optional: Schedule the Tool with Cron

The tool can be scheduled using `cron`.

Open crontab:

```bash
crontab -e
```

Example — archive every day at 1 AM:

```cron
0 1 * * * /home/user/log-archive-tool/log-archive /var/log >> /home/user/log-archive-tool/archive.log 2>&1
```

Check configured cron jobs:

```bash
crontab -l
```

---

# 🏢 DevOps Production Use Case

A typical production environment may look like:

```text
                Linux Server
                     |
              Application Logs
                     |
                Log Rotation
                     |
              Archive / Compress
                     |
              +------+------+
              |             |
             S3          Backup Storage
              |
       Long-Term Retention
```

For larger production environments, logs may instead be forwarded to:

```text
Application
     |
     v
Fluent Bit / Filebeat
     |
     v
Centralized Logging
     |
     +---- Elasticsearch
     |
     +---- Loki
     |
     +---- CloudWatch
```

The Bash project is therefore a foundation for understanding more advanced log-management systems.

---

# ⭐ Future Enhancements

The basic project can be extended with additional features.

### Version 1 — Basic

```text
CLI
 |
tar.gz
 |
Archive
```

### Version 2 — Timestamping

```text
CLI
 |
Timestamp
 |
tar.gz
 |
Archive
```

### Version 3 — Scheduled Archiving

```text
Cron
 |
Script
 |
Archive
```

### Version 4 — Cloud Backup

```text
Script
 |
tar.gz
 |
AWS S3
```

### Version 5 — Production Logging

```text
Application
 |
Log Files
 |
Log Rotation
 |
Compression
 |
S3
 |
Lifecycle Policy
 |
Long-Term Storage
```

---

# ☁️ Optional AWS S3 Integration

A production-style enhancement is uploading completed archives to Amazon S3.

Example:

```bash
aws s3 cp archives/logs_archive_20260917_101530.tar.gz s3://my-log-archive-bucket/
```

This provides remote storage instead of keeping every archive on the application server.

---

# 📊 Useful Linux Commands

### List logs

```bash
ls -lh /var/log
```

### Check disk usage

```bash
df -h
```

### Check directory size

```bash
du -sh /var/log
```

### Find large log files

```bash
find /var/log -type f -size +100M
```

### View recent logs

```bash
tail -n 100 /var/log/syslog
```

### Follow a log

```bash
tail -f /var/log/syslog
```

### Search logs

```bash
grep -i "error" /var/log/syslog
```

---

# 📚 Learning Objectives

After completing this project, you should understand:

### Linux

* Linux filesystem
* `/var/log`
* File permissions
* Directory management
* Disk usage

### Bash

* Script arguments
* Variables
* Conditions
* Exit codes
* Command substitution
* File tests
* Error handling

### CLI

* Command-line arguments
* Usage messages
* Exit status
* Automation

### Archiving

* `tar`
* gzip compression
* `.tar.gz`
* Archive extraction

### DevOps

* Log management
* Server maintenance
* Automation
* Cron
* Backup concepts
* Storage management

---

# 🎯 Interview Questions

### 1. What is `/var/log`?

`/var/log` is a common Linux directory used for storing system and application log files.

---

### 2. What is the difference between `tar` and `gzip`?

`tar` primarily combines files/directories into an archive, while `gzip` compresses data.

A `.tar.gz` file commonly means:

```text
Files
  ↓
tar archive
  ↓
gzip compression
  ↓
.tar.gz
```

---

### 3. How do you create a tar.gz archive?

```bash
tar -czf archive.tar.gz /path/to/logs
```

---

### 4. How do you list the contents of a tar.gz file?

```bash
tar -tzf archive.tar.gz
```

---

### 5. How do you extract a tar.gz file?

```bash
tar -xzf archive.tar.gz
```

---

### 6. How do you check disk space?

```bash
df -h
```

---

### 7. How do you find large log files?

```bash
find /var/log -type f -size +100M
```

---

### 8. How would you prevent logs from filling the disk?

A production solution could include:

```text
Log Rotation
     ↓
Compression
     ↓
Retention Policy
     ↓
Centralized Logging
     ↓
Cloud/Object Storage
```

Linux `logrotate`, centralized logging, and storage lifecycle policies are common production approaches.

---

# 🏆 Project Skills

```text
Linux
Bash
Shell Scripting
CLI
File Management
Directory Management
Tar
Gzip
Log Management
Log Archiving
Cron
Linux Permissions
Automation
Troubleshooting
DevOps
```

---

# 📌 GitHub Repository Description

Use this as the GitHub repository description:

```text
A Bash CLI tool to compress and archive Linux log files into timestamped tar.gz archives.
```

### Suggested Repository Name

```text
log-archive-tool
```

### Suggested GitHub Topics

```text
linux
bash
shell-scripting
devops
log-management
log-archive
tar
gzip
cron
linux-administration
automation
cli
```

---

# 🏁 Conclusion

The **Log Archive Tool** is a simple but practical Linux/Bash project that demonstrates how to automate log management from the command line.

It provides a foundation for more advanced DevOps practices such as:

```text
Bash
  ↓
Cron
  ↓
Log Rotation
  ↓
Compression
  ↓
AWS S3
  ↓
Retention
  ↓
Centralized Logging
  ↓
Monitoring & Alerting
```

This project is suitable as a **beginner Linux/Bash project** and can later be expanded into a production-oriented log management and backup solution.
