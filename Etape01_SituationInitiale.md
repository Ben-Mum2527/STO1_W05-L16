# Etape 01 - Situation initiale

## Objectifs

* Situation de départ

Il n'y a pas encore de RAID à cette étape. Toutes les données sont stockées sur le bucket S3.

* Situation à atteindre

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Windows|0|2|20|15|


## Pré-requis

Les pré-requis nécéssaires pour cette étape sont: 

- Machine windows avec 3 disques de 15 Go dédiés au RAID
- Un Bucket S3 avec des données de test 

## Analyse

La réalisation de cette situation initiale se fera par ces étapes: 

1. Création d'un RAID0 via un script sur la machine windows
2. Copier les données du Bucket S3 vers le nouveau RAID.
3. Test d'intégrité des données par comparaison des hashs entre données source et la copie



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
