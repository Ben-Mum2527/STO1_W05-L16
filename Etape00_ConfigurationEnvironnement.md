# Etape 00 - Configuration des environnements

## Objectifs

Mise en place :

- Une machine virtuelle Windows accessible via RDP avec 3 disques utilisés pour la création d’un RAID 0 puis d’un RAID 5

- Une machine virtuelle Linux accessible par SSH avec 4 disques utilisés pour la création d’un RAID 1 puis d’un RAID 6

## Pré-requis

- Logiciel de virtualisation (VMWare)
- Accès internet
- Accès à un Bucket AWS S3


## Valider les accès à l'infrastructure

### Accès à l'instance linux



```bash
Par SSH: 
    Commande : raidlinux@192.168.253.133
    Password : P@$$w0rd

```

### Accès l'instance windows

```bash
Par RDP : 
    IP: 192.168.30.136
    Utilisateur : winaccess
    Password: P@$$w0rd

```

### Connection internet sortante

```bash
Machine Linux: Connexion en NAT avec l'IP du PC physique
```

```bash
Machine Windows: Connexion en NAT avec l'IP du PC physique
```

### Volumes nécessaires pour la première étape du projet

```bash
Machine windows: 2 disques de 10GB
```

```bash
Machine Linux: 2 disques de 20GB
```

### Accès aux différents buckets

#### Bucket contenant les données du client

```bash
s3://sto1-project-data
```

#### Bucket "temporaire" pour la migration

```bash
//TODO INPUT
```

```bash
s3://sto1-corentin
```

## Installation des dépendances

### CLI d'AWS

#### Sous Windows

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

#### Sous Linux

```bash
#Installer le paquet awscli
 sudo apt install awscli

#Vérifier que l'installation a réussi
 aws --version
 #Output attendu
 aws-cli/2.9.19 Python/3.11.2 Linux/6.1.0-40-amd64 source/x86_64.debian.12
```

```bash
#Créer config par défaut AWS
 aws configure

 AWS Access Key ID : #Entrer AccessKeyId donné
 AWS Secret Access Key : #Entrer SecretAccessKey donné
 Default region name [None]: #Valider
 Default output format [none]: #Entrer "json"
```
```bash
#Paramétrer le profil sto1
#Modifier le fichier credentials sous .aws
 sudo nano .aws/credentials

#Remplacer la config [default] par la config suivante:
 [sto1]
 aws_access_key_id = VotreAccessKeyId
 aws_secret_access_key = VotreSecretAccessKey

#Tester la config
#Accéder à votre répertoire S3 avec le profil sto1
 aws s3 ls s3://sto1-corentin --profile sto1
 #Output attendu: Tous les fichiers présents dans le répertoire S3
 2025-09-15 15:50:53   Mario.jpg
```
### Logiciel RAID

#### Sous Windows

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

#### Sous Linux

```bash
Utilitaire mdadm
```

### Language de scripting

#### Sous Windows

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

#### Sous Linux

```bash
BASH
```

