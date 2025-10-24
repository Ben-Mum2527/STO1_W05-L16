# Etape 05 - Nettoyage

## Objectifs

* Nettoyer la trace des anciens raids
* Nettoyer les données temporaires de la migration (sur les disques comme sur le bucket de votre équipe)

## Pré-requis

//TODO - expliquer les pré-requis nécessaires en début d'intervention pour cette étape

## Analyse

//TODO expliquer l'approche qui va être favorisée, sources à l'appui

## TODO

### Nettoyage sur l'instance initiale

```bash
//TODO INPUT
```

```bash
//TODO OUTPUT
```

### Nettoyage sur l'instance finale

```bash
//TODO OUTPUT
```

### Nettoyage sur le bucket de votre équipe

```bash
#Supprimer toutes les données du bucket
aws s3 rm --recursive s3://sto1-corentin/ --profile sto1

#Checker si tout est supprimé
aws s3 ls s3://sto1-corentin/ --profile sto1
```

## Problèmes techniques non-résolus

//TODO ajouter ici les liens pointant vers les issues concernées

## Feedback

//TODO expliquer le retour d'expérience (erreurs, comportement inattendu, changement de stratégies)
