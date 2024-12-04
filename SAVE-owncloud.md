
````
#!/bin/bash

# Variables
BASE_DIR="/var/lib/docker/volumes/030ba89a9b5c607c7a87069aa0307a0b8819521ee5b469338eaee4129dd3e74f/_data"
TOIP_DIR="$BASE_DIR/toip"
ARCHIVE_DIR="$BASE_DIR/archive"
DATE=$(date '+%d-%m-%Y_%H:%M:%S')
FTP_SERVER="adresse_du_serveur_ftp"
FTP_USER="votre_utilisateur_ftp"
FTP_PASS="votre_mot_de_passe"
FTP_DIR="/path/to/archives_toip"

# Création des répertoires si nécessaires
mkdir -p $TOIP_DIR
mkdir -p $ARCHIVE_DIR

# Sauvegarde locale du fichier CSV
cp $TOIP_DIR/data.csv $ARCHIVE_DIR/sio2-$DATE.csv

# Compression du répertoire toip
zip -r $ARCHIVE_DIR/sio2-$DATE.zip $TOIP_DIR

# Transfert du fichier ZIP sur le serveur FTP
curl -T $ARCHIVE_DIR/sio2-$DATE.zip ftp://$FTP_USER:$FTP_PASS@$FTP_SERVER$FTP_DIR/

````