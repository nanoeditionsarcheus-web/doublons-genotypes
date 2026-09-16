# Doublons de génotypes

Un outil pour repérer les individus en double dans une matrice de génotypes microsatellites.

**→ [Ouvrir l'outil](https://nanoeditionsarcheus-web.github.io/doublons-genotypes/)**

---

## Ce que ça fait

L'outil compare tous les individus **deux à deux** et compte, pour chaque paire, le nombre de locus identiques. Les vrais doublons se détachent d'eux-mêmes : ils forment une petite grappe de paires identiques sur la totalité des locus, nettement séparée du reste.

Il gère les locus à **2, 3 ou 4 allèles**, mélangés dans un même fichier — utile lorsque certains individus présentent des allèles surnuméraires à certains locus (hybridation, introgression, polyploïdie partielle). Le nombre d'allèles est déduit automatiquement, locus par locus.

Il affiche :

- la répartition complète des paires selon le nombre de locus partagés ;
- l'étendue du nombre d'allèles par locus détecté dans le fichier ;
- la liste des paires retenues, avec le nombre de locus comparés et de locus divergents ;
- les identifiants qui apparaissent plus d'une fois dans le fichier ;
- les génotypes manquants et ceux dont les allèles sont en ordre décroissant.

Les résultats s'exportent en CSV.

## Comment s'en servir

1. Coller la matrice dans la zone de texte, ou ouvrir un fichier. On peut copier-coller directement depuis Excel ; la ligne d'en-tête est ignorée automatiquement.
2. Choisir le seuil : **au moins** *k* locus identiques pour trouver les doublons et les quasi-doublons, **exactement** *k* pour reproduire le comportement de la feuille Maple d'origine.
3. Cliquer sur **Chercher les doublons**.

## Format des données

Une ligne par individu : l'identifiant, puis les génotypes. Chaque allèle est scoré sur trois chiffres, donc un locus s'écrit en chiffres collés :

| Allèles au locus | Chiffres | Exemple |
|---|---|---|
| 2 (diploïde) | 6 | `163175` |
| 3 | 9 | `163175188` |
| 4 | 12 | `163175188200` |

```
1974	147167	168168	188192	169193	169177	167167	178178	165189	151151	157173
1993	155171187	144144	188188	169197	161169	167187191219	178182	169169	147151	157169
```

Les allèles séparés par `/`, `-` ou `|` sont aussi acceptés (`163/175/188`). Le séparateur de colonnes — tabulation, virgule, point-virgule ou espaces — est détecté automatiquement. Les en-têtes et les colonnes qui ne sont pas des génotypes sont ignorés. Les données manquantes sont codées avec des zéros (`000000`, `000000000`…) par défaut, et ce code est modifiable.

## Deux réglages qui changent le résultat

**Ignorer l'ordre des allèles.** Avec cette option, `192176` et `176192` sont reconnus comme le même génotype. Sans elle, la comparaison est strictement littérale.

**Écarter les locus manquants.** Un locus absent chez l'un des deux individus est retiré du décompte pour cette paire, plutôt que compté comme identique. La colonne « locus comparés » indique alors le nombre réel de locus ayant servi à la comparaison.

## Vos données restent chez vous

Tout le calcul se fait dans le navigateur. Aucune donnée n'est envoyée nulle part : la page est servie une fois, puis fonctionne seule. Le code est lisible en entier dans ce dépôt.

Pour un usage entièrement hors ligne, faites *Enregistrer la page sous* dans votre navigateur, ou téléchargez `index.html` : le fichier fonctionne tel quel, par simple double-clic, sur Mac comme sur PC. Aucune installation n'est requise.

## Origine

L'algorithme et la méthode sont de **Pierre Duchesne**, à partir de sa feuille de calcul Maple *CALCUL DOUBLONS*. La logique d'origine (locus diploïdes) est reprise fidèlement : sur le jeu d'essai de la feuille (13 individus, 11 locus, seuil de 3 locus identiques), l'outil retrouve exactement les mêmes trois paires et les mêmes quatre individus.

S'y ajoutent la prise en charge des locus à 3 et 4 allèles, le traitement des données manquantes, la normalisation de l'ordre des allèles, la répartition d'ensemble et l'export CSV.

## Écriture

Cet outil a été écrit par **Claude** (Anthropic), à partir de la feuille Maple et de jeux de données réels, dans le cadre d'un échange avec Éleine Leblanc. La traduction a été vérifiée contre les résultats que Maple avait conservés dans la feuille d'origine, et l'extension multi-allèles contre les fichiers de test fournis.

L'algorithme demeure celui de Pierre Duchesne.
