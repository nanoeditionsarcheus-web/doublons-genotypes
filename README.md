# Doublons de génotypes

Un outil pour repérer les individus en double dans une matrice de génotypes microsatellites.

**→ [Ouvrir l'outil](https://nanoeditionsarcheus-web.github.io/doublons-genotypes/)**

* * *

## Ce que ça fait

L'outil compare tous les individus **deux à deux** et compte, pour chaque paire, le nombre de locus identiques. Les vrais doublons se détachent d'eux-mêmes : ils forment une petite grappe de paires identiques sur la totalité des locus, nettement séparée du reste.

Il affiche :

* la répartition complète des paires selon le nombre de locus partagés ;
* la liste des paires retenues, avec le nombre de locus comparés et de locus divergents ;
* les identifiants qui apparaissent plus d'une fois dans le fichier ;
* les génotypes manquants et ceux dont les allèles sont en ordre décroissant.

Les résultats s'exportent en CSV.

## Comment s'en servir

1. Coller la matrice dans la zone de texte, ou ouvrir un fichier.
2. Choisir le seuil : **au moins** *k* locus identiques pour trouver les doublons et les quasi-doublons, **exactement** *k* pour reproduire le comportement de la feuille Maple d'origine.
3. Cliquer sur **Chercher les doublons**.

## Format des données

Une ligne par individu : l'identifiant, puis les génotypes à six chiffres.

    1    143163    168168    188192    169197    173177    167167    174178    149169    155183    153157
    2    151187    168208    188208    177197    161177    159235    182218    149161    155195    157157

Le séparateur — tabulation, virgule, point-virgule ou espaces — est détecté automatiquement. Les lignes d'en-tête et les colonnes qui ne sont pas des génotypes sont ignorées. Les données manquantes sont codées `000000` par défaut, et ce code est modifiable.

## Deux réglages qui changent le résultat

**Ignorer l'ordre des allèles.** Avec cette option, `192176` et `176192` sont reconnus comme le même génotype. Sans elle, la comparaison est strictement littérale.

**Écarter les locus manquants.** Un locus absent chez l'un des deux individus est retiré du décompte pour cette paire, plutôt que compté comme identique. La colonne « locus comparés » indique alors le nombre réel de locus ayant servi à la comparaison.

## Vos données restent chez vous

Tout le calcul se fait dans le navigateur. Aucune donnée n'est envoyée nulle part : la page est servie une fois, puis fonctionne seule. Le code est lisible en entier dans ce dépôt.

Pour un usage entièrement hors ligne, faites *Enregistrer la page sous* dans votre navigateur, ou téléchargez `index.html` : le fichier fonctionne tel quel, par simple double-clic, sur Mac comme sur PC. Aucune installation n'est requise.

## Origine

L'algorithme et la méthode sont de **Pierre Duchesne**, à partir de sa feuille de calcul Maple *CALCUL DOUBLONS*. Cette version en reprend la logique fidèlement : sur le jeu d'essai de la feuille d'origine (13 individus, 11 locus, seuil de 3 locus identiques), elle retrouve exactement les mêmes trois paires et les mêmes quatre individus.

S'y ajoutent le traitement des données manquantes, la normalisation de l'ordre des allèles, la répartition d'ensemble et l'export CSV.

## Écriture

Cette version a été écrite par **Claude** (Anthropic), à partir de la feuille Maple et d'un jeu de données réel, dans le cadre d'un échange avec Éleine Leblanc. La traduction a été vérifiée contre les résultats que Maple avait conservés dans la feuille d'origine.

L'algorithme demeure celui de Pierre Duchesne.
