


!/bin/bash


SOURCE_DIR="/home/sasaskm/desktop_management"


BACKUP_DIR="/home/sasaskm/backup1"

mkdir -p "$BACKUP_DIR"


TIMESTAMP=$(date +'%Y%m%d_%H%M%S')


BACKUP_FILE="backup_${TIMESTAMP}.tar.gz"


LOG_FILE="$BACKUP_DIR/backup.log"


FILES_TO_BACKUP=$(find "$SOURCE_DIR" -type f \( -name "*.pdf" -o -name "*.txt" \) -mtime -7)

if [ -z "$FILES_TO_BACKUP" ]; then
    echo "$TIMESTAMP - Tidak ditemukan file yang memenuhi kriteria backup." >> "$LOG_FILE"
    echo "Backup gagal: tidak ada file yang sesuai kriteria."
    exit 1
fi


tar -czf "$BACKUP_DIR/$BACKUP_FILE" $FILES_TO_BACKUP


if [ $? -eq 0 ]; then
    echo "$TIMESTAMP - Backup berhasil: $BACKUP_FILE dibuat." >> "$LOG_FILE"
    echo "Backup berhasil: $BACKUP_FILE"
else
    echo "$TIMESTAMP - Backup gagal." >> "$LOG_FILE"
    echo "Backup gagal."
    exit 1
fi



