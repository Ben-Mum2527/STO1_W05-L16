# Etape 04 - 3ème migration

## Objectifs

* Situation de départ

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Linux|1|2|20|20|

* Situation à atteindre

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Linux|6|4|40|40|


## Pré-requis

- Un RAID 1 fonctionnel

## Analyse

Après recherche, nous avons constaté que le risques de pertes de données pour passer d'un RAID 1 à un RAID 5 puis un RAID 6 ne sont pas négligables.

Nous avons donc optés pour faire un backup des données sur stockage temporaire.

Un test d'intégrité des données sera réalisé à la fin du processus. 

- Copie des données du RAID 1 dans une solution de stockage temporaire
- Supprimer le RAID 1
- Créer un RAID 6
- Copier les données depuis le stockage externe vers le RAID 6
- Faire un test d'intégrité des données


## TODO

### Configuration du RAID de départ

#### Mise en place

```bash
#Obtenir les hashs de tous les fichiers présents dans le dossier /media/raid1/
cd /media/raid1
find . -type f -exec sha256sum {} \;| sort -z > "hashes.txt"
sudo mv hashes.txt /media

#Copier tous les fichiers du raid1 sur le stockage S3
aws s3 cp /media/raid1/ s3://sto1-corentin/ --recursive --profile sto1

#Vérifier que le S3 a bien les fichiers
aws s3 ls s3://sto1-corentin/ --profile sto1
```

```bash
#Supprimer le RAID1
#Démonter le point de montage
sudo umount /dev/md127

#Enlever le montage automatique
#Supprimer la ligne ajoutée dans fstab
sudo nano /etc/fstab

#Arrêter le RAID
sudo mdadm --stop /dev/md127

#Réinitialiser les deux disques du RAID1
sudo mdadm --zero-superblock /dev/sdb
sudo mdadm --zero-superblock /dev/sdc

#Vérifier que les disques sont libres
lsblk
#Output
sdb      8:16   0   20G  0 disk
sdc      8:32   0   20G  0 disk

#Supprimer le répertoire RAID1
sudo rm -r /media/raid1/
```

### Configuration du RAID souhaité

#### Mise en place

- Ajouter 2 disques de 20 GB à la machine

```bash
#Checker les disques disponibles
 lsblk
 #Output
sda      8:0    0   10G  0 disk
├─sda1   8:1    0  3.6G  0 part /
├─sda2   8:2    0    1K  0 part
├─sda5   8:5    0  976M  0 part [SWAP]
└─sda6   8:6    0  5.4G  0 part /home
sdb      8:16   0   20G  0 disk
sdc      8:32   0   20G  0 disk
sdd      8:48   0   20G  0 disk
sde      8:64   0   20G  0 disk

#Noter que les deux diques que l'on va utiliser sont: sdb et sdc, sdd et sde
```

```bash
# Création du RAID 6 :
sudo mdadm --create /dev/md6 --level=6 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde

# Choisir le format de stockage du RAID :
sudo mkfs -t ext4 /dev/md6

# Créer le point de montage du RAID :
sudo mkdir /media/raid6

#Changer les droits du dossier
sudo chown -R raidlinux:raidlinux /media/raid6

# Obtenir l’ID du RAID créé et le copier :
sudo blkid -o value -s UUID /dev/md6

// Exemple de sortie :
-----------------------------------
566732e7-dff1-47bc-845f-9a36c51109a1

# Ouvrir le fstab de l'OS
sudo nano /etc/fstab

# Ajouter la ligne avec l'uid du RAID:
UUID=566732e7-dff1-47bc-845f-9a36c51109a1 /media/raid6 ext4 rw,discard,errors=remount-ro,x-systemd.growfs 0 1
```



#### Validation technique

```bash
#Redémarrer la machine
# Pour voir si le disque raid a été monté
mount | grep "raid6"
#output
/dev/md127 on /media/raid6 type ext4 (rw,relatime,discard,errors=remount-ro,stripe=256,x-systemd.growfs)

# Vérifier que les bons disques sont dans le RAID
lsblk 
#Output
sdb       8:16   0   20G  0 disk
└─md127   9:127  0   40G  0 raid6 /media/raid6
sdc       8:32   0   20G  0 disk
└─md127   9:127  0   40G  0 raid6 /media/raid6
sdd       8:48   0   20G  0 disk
└─md127   9:127  0   40G  0 raid6 /media/raid6
sde       8:64   0   20G  0 disk
└─md127   9:127  0   40G  0 raid6 /media/raid6
```

#### Validation métier

```bash
aws s3 sync s3://sto1-corentin /media/raid6/ --profile sto1
```

```bash
#Créer un fichier contenant les hashs des fichiers téléchargés
cd /media/raid6
find . -type f -exec sha256sum {} \;| sort -z > "hashes.txt"
mv hashes.txt hashes1.txt
sudo mv hashes1.txt /media

#Comparer les deux fichiers de hash et voir s'ils sont différents
cmp hashes.txt hashes1.txt || echo "files are different"
```

## Problèmes techniques non-résolus

//TODO ajouter ici les liens pointant vers les issues concernées

## Feedback

Vu que nous n'arrivions pas à accéder aux hashs des fichiers sur le S3 nous avons créer leurs hashs une fois sur la machine locale et nous comparons les hashs des fichiers une fois qu'ils sont stockés sur le RAID 1 et sur le RAID 6.
