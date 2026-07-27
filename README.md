https://roadmap.sh/projects/log-archive-tool

#!/bin/bash

# Check if log directory is provided
if [ $# -ne 1 ]; then
    echo "Usage: $0 <log-directory>"
    exit 1
fi

LOG_DIR=$1

# Check if directory exists
if [ ! -d "$LOG_DIR" ]; then
    echo "Error: Directory does not exist!"
    exit 1
fi

ARCHIVE_DIR="archive_logs"
mkdir -p "$ARCHIVE_DIR"

TIMESTAMP=$(date +"%Y%m%d_%H%M%S")

ARCHIVE_NAME="logs_archive_${TIMESTAMP}.tar.gz"

tar -czf "$ARCHIVE_DIR/$ARCHIVE_NAME" -C "$LOG_DIR" .

# Delete archives older than 30 days
find "$ARCHIVE_DIR" -type f -name "*.tar.gz" -mtime +30 -exec rm -f {} \;

echo "Old archives (older than 30 days) deleted."

echo "$(date): Archived $LOG_DIR -> $ARCHIVE_DIR/$ARCHIVE_NAME" >> archive_history.log

echo "====================================="
echo "Archive created successfully!"
echo "File: $ARCHIVE_DIR/$ARCHIVE_NAME"
echo "Archive Size:"
du -sh "$ARCHIVE_DIR/$ARCHIVE_NAME"
echo "====================================="
