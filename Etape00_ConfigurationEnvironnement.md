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
    Commande : linaccess@192.168.15.136
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
Machine Linux: 2 disques de 10GB
```

```bash
Machine Linux: 2 disques de 10GB
```

### Accès aux différents buckets

#### Bucket contenant les données du client

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

#### Bucket "temporaire" pour la migration

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
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
//TODO INPUT
```

```bash
//TODO OUTPUT
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
//TODO INPUT
```

```bash
//TODO OUTPUT
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
//TODO INPUT
```

```bash
//TODO OUTPUT
```
