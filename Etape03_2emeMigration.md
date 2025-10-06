# Etape 03 - 2ème migration

## Objectifs

* Situation de départ

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Windows|5|3|45|25|

* Situation à atteindre

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Linux|1|2|15|15|


## Pré-requis

- Un RAID 5 sur une machine Windows
- Un Bucket S3 pour la migration inter-machines
- Une machine Linux avec 2 disks de 10 Go non-utilisés

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
//TODO INPUT
```

```bash
//TODO OUTPUT
```


#### Validation technique

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

#### Validation métier

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

## Problèmes techniques non-résolus

//TODO ajouter ici les liens pointant vers les issues concernées

## Feedback

//TODO expliquer le retour d'expérience (erreurs, comportement inattendu, changement de stratégies)
