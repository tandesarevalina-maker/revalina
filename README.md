# revalina
### b. Isi script berikut lengkap dengan komentar:


#!/bin/bash

# Direktori sumber file yang akan dibackup
SOURCE_DIR="/home/rahmatnusi/project_file_management"

# Direktori tujuan backup
BACKUP_DIR="/home/rahmatnusi/backup1"

# Membuat direktori backup jika belum ada
mkdir -p "$BACKUP_DIR"

# Timestamp untuk nama file backup dan pencatatan log
TIMESTAMP=$(date +'%Y%m%d_%H%M%S')

# Nama file backup dengan timestamp
BACKUP_FILE="backup_${TIMESTAMP}.tar.gz"

# File log aktivitas backup
LOG_FILE="$BACKUP_DIR/backup.log"

# Cari file .pdf atau .txt yang dimodifikasi 7 hari terakhir
FILES_TO_BACKUP=$(find "$SOURCE_DIR" -type f \( -name "*.pdf" -o -name "*.txt" \) -mtime -7)

# Jika tidak ada file yang memenuhi kriteria, tulis log dan keluar
if [ -z "$FILES_TO_BACKUP" ]; then
    echo "$TIMESTAMP - Tidak ditemukan file yang memenuhi kriteria backup." >> "$LOG_FILE"
    echo "Backup gagal: tidak ada file yang sesuai kriteria."
    exit 1
fi

# Membuat file backup terkompresi (tar.gz) dari file hasil pencarian
tar -czf "$BACKUP_DIR/$BACKUP_FILE" $FILES_TO_BACKUP

# Mengecek hasil perintah tar, tulis log dan notifikasi
if [ $? -eq 0 ]; then
    echo "$TIMESTAMP - Backup berhasil: $BACKUP_FILE dibuat." >> "$LOG_FILE"
    echo "Backup berhasil: $BACKUP_FILE"
else
    echo "$TIMESTAMP - Backup gagal." >> "$LOG_FILE"
    echo "Backup gagal."
    exit 1
fi


### c.
