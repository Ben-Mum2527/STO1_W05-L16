# Etape 03 - 2ème migration

## Objectifs

* Situation de départ

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Windows|5|3|45|25|

* Situation à atteindre

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Linux|1|2|20|20|


## Pré-requis

- Un RAID 5 sur une machine Windows
- Un Bucket S3 pour la migration inter-machines
- Une machine Linux avec 2 disks de 20 Go non-utilisés

## Analyse

À cette étape il faut passer un Bucket S3 pour la migration entre les deux machines.

- Migrer les données depuis le RAID 5 vers le Bucket
- Tester l'intégrité des données
- Créer le RAID 1 sur la machine Linux
- Migrer les données depuis le Bucket sur le nouveau RAID 1
- Tester à nouveau l'intégrité des données


## TODO

### Configuration du RAID de départ

#### Mise en place

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

### Configuration du RAID souhaité

#### Mise en place

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

#Noter que les deux diques que l'on va utiliser sont: sdb et sdc
```

```bash
# Avoir mdadm (outil de gestion RAID) :
sudo apt-get install mdadm -y

# Création du RAID 1 :
sudo mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdb /dev/sdc

# Choisir le format de stockage du RAID :
sudo mkfs -t ext4 /dev/md1

# Créer le point de montage du RAID :
sudo mkdir /media/raid1

#Modifier droit du fichier
sudo chown -R raidlinux:raidlinux /media/raid1

# Obtenir l’ID du RAID créé et le copier :
sudo blkid -o value -s UUID /dev/md1

// Exemple de sortie :
-----------------------------------
566732e7-dff1-47bc-845f-9a36c51109a1

# Ouvrir le fstab de l'OS
sudo nano /etc/fstab

# Ajouter la ligne avec l'uid du RAID:
UUID=566732e7-dff1-47bc-845f-9a36c51109a1 /media/raid1 ext4 rw,discard,errors=remount-ro,x-systemd.growfs 0 1
```


#### Validation technique

```bash
#Redémarrer la machine
# Pour voir si le disque raid a été monté
mount | grep "raid1"
/dev/md127 on /media/raid1 type ext4 (rw,relatime,discard,errors=remount-ro,x-systemd.growfs)

# Vérifier que les bons disques sont dans le RAID
lsblk 
sdb       8:16   0   20G  0 disk
└─md127   9:127  0   20G  0 raid1 /media/raid1
sdc       8:32   0   20G  0 disk
└─md127   9:127  0   20G  0 raid1 /media/raid1
```


#### Validation métier

```bash
aws s3 sync s3://sto1-project-data /media/raid1/ --profile sto1
```


## Problèmes techniques non-résolus

//TODO ajouter ici les liens pointant vers les issues concernées

## Feedback

Normalement, nous voulions contrôler l'intégrité des données. Mais, après quelques tests nous avons remarqué que le serveur S3 n'arrivait à nous fournir les hashs de tous les fichiers. Nous avons donc mis de côté cette étape car nous pensons que certains fichiers sont obsolètes.
