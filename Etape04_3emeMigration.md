# Etape 04 - 3ème migration

## Objectifs

* Situation de départ

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Linux|1|2|15|15|

* Situation à atteindre

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Linux|6|4|30|30|


## Pré-requis

- Un RAID 1 fonctionnel

## Analyse

Après recherche, nous avons constaté que le risques de pertes de données pour passer d'un RAID 1 à un RAID 5 puis un RAID 6 ne sont pas négligables.

Nous avons donc optés pour faire un backup des données sur stockage temporaire.

Un test d'intégrité des données sera réalisé à la fin de processus. 

- Copie des données du RAID 1 dans une solution de stockage temporaire
- Supprimer le RAID 1
- Créer un RAID 6
- Copier les données depuis le stockage externe vers le RAID 6
- Faire un test d'intégrité des données


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
