
````
# Chemins et configurations
SOURCE_DIR="/var/lib/docker/volumes/030ba89a9b5c607c7a87069aa0307a0b8819521ee5b469338eaee4129dd3e74f/_data/toip/"
BACKUP_DIR="/backup_owncloud"
DATE=$(date +"%d-%m-%Y_%H:%M:%S")
BACKUP_FILE="$BACKUP_DIR/sio2-$DATE.zip"
FTP_SERVER="192.168.20.150"
FTP_USER="root"
FTP_PASS="sio2024"
REMOTE_DIR="/remote_backup"

# Vérifier que le répertoire source existe
if [ ! -d "$SOURCE_DIR" ]; then
    echo "Erreur : le répertoire source $SOURCE_DIR n'existe pas."
    exit 1
fi

# Créer le répertoire de sauvegarde s'il n'existe pas
mkdir -p "$BACKUP_DIR"

# Compresser le contenu du répertoire source dans un fichier ZIP
zip -r "$BACKUP_FILE" "$SOURCE_DIR" > /dev/null 2>&1

# Vérifier si la compression a réussi
if [ $? -eq 0 ]; then
    echo "Sauvegarde réussie : $BACKUP_FILE"
else
    echo "Erreur lors de la création de la sauvegarde."
    exit 1
fi

# Transférer le fichier ZIP vers le serveur FTP
curl -T "$BACKUP_FILE" ftp://$FTP_USER:$FTP_PASS@$FTP_SERVER$REMOTE_DIR/ --ftp-create-dirs

# Vérifier si le transfert a réussi
if [ $? -eq 0 ]; then
    echo "Transfert réussi vers ftp://$FTP_SERVER$REMOTE_DIR/"
else
    echo "Erreur lors du transfert vers le serveur FTP."
    exit 1
fi
#!/bin/bash
apt install zip
# Chemins et configurations
SOURCE_DIR="/var/lib/docker/volumes/030ba89a9b5c607c7a87069aa0307a0b8819521ee5b469338eaee4129dd3e74f/_data/toip/"
BACKUP_DIR="/backup_owncloud"
DATE=$(date +"%d-%m-%Y_%H:%M:%S")
BACKUP_FILE="$BACKUP_DIR/sio2-$DATE.zip"

# Vérifier que le répertoire source existe
if [ ! -d "$SOURCE_DIR" ]; then
    echo "Erreur : le répertoire source $SOURCE_DIR n'existe pas."
    exit 1
fi

# Créer le répertoire de sauvegarde s'il n'existe pas
mkdir -p "$BACKUP_DIR"

# Compresser le contenu du répertoire source dans un fichier ZIP
zip -r "$BACKUP_FILE" "$SOURCE_DIR" > /dev/null 2>&1

# Vérifier si la compression a réussi
if [ $? -eq 0 ]; then
    echo "Sauvegarde réussie : $BACKUP_FILE"
else
    echo "Erreur lors de la création de la sauvegarde."
    exit 1
fi



````