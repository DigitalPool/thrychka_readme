# Folder Synchronization Script

A Python script that synchronizes the contents of a source folder with a replica folder. It continuously monitors changes, updates files and directories accordingly, and removes items in the replica that no longer exist in the source. All actions are logged for tracking purposes.

## Features

- **Automatic Sync:** Continuously monitors the source folder and updates the replica in real-time.
- **Efficient Copying:** Copies new files and updates existing ones if the source version is newer.
- **Orphan Removal:** Deletes files and directories from the replica that do not exist in the source.
- **Logging System:** Automatically generates a log file (`logfile.log`) to record synchronization activities.
- **Command-Line Support:** Easily configure source, replica, sync interval, and log file directory via command-line arguments.

## Requirements

- Python 3.x (only standard libraries used: `sys`, `os`, `time`, `shutil`, `argparse`, and `logging`).

## How It Works

1. **Logging Setup (`add_logfile`):**
   - Creates the specified log directory if it doesn’t exist.
   - Initializes a log file to record all sync operations.

2. **File and Folder Synchronization (`copying_from_src`):**
   - Ensures the replica folder exists.
   - Iterates through the source folder:
     - **Files:** Copies missing or updated files to the replica.
     - **Directories:** Copies new directories and updates contents recursively.

3. **Cleanup Process (`delete_from_dest`):**
   - Scans the replica folder:
     - **Files:** Deletes those not present in the source.
     - **Directories:** Removes directories (or parts of them) missing in the source.

4. **Continuous Syncing (`main`):**
   - Runs in an infinite loop to maintain synchronization at a user-defined interval.
   - Gracefully stops when interrupted via `Ctrl+C`.

## Usage

### Command-Line Arguments

The script requires the following arguments:

1. **source** – Path to the source folder.
2. **replica** – Path to the replica folder.
3. **interval** – Synchronization interval (seconds).
4. **logfile** – Directory to store the log file.

### Example Usage

```bash
python sync.py /path/to/source /path/to/replica 10 /path/to/logs
