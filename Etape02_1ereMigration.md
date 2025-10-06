# Etape 02 - 1ère migration

## Objectifs

* Situation de départ

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Windows|0|3|45|40|

* Situation à atteindre

|OS |RAID|Nb volumes|Capacité totale|Capacité résiduelle|
|:--|:-- |:--       |:--            |:--|
|Windows|5|3|30|25|


## Pré-requis

- Avoir un RAID 0 fonctionnel

## Analyse

Il est très compliqué de migrer d'un RAID 0 à un RAID 5 sans perte de données. On peut cependant passer les données dans une solution de stockage temporaire.

Les étapes pour la migration seraient donc les suivantes: 

- Copie des données du RAID 0 dans une solution de stockage temporaire
- Supprimer le RAID 0
- Créer un RAID 5
- Copier les données depuis le stockage externe vers le RAID 5
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
