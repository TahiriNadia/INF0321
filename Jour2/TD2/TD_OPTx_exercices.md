# Exercices : Estimations de performances d’accès disque

Pour les estimations suivantes, utilisez les paramètres du tableau ci-dessous. On considère une base de données relationnelle avec deux tables : `Prêt` et `Membre`, organisées de façon **sérielle**.

## Paramètres des disques

| Paramètre          | Signification                                                            |
|--------------------|--------------------------------------------------------------------------|
| `TempsESDisque(n)` | Temps total de transfert (lecture ou écriture) de *n* octets             |
| `TempsTrans(n)`    | Temps de transfert de *n* octets sans repositionnement                   |
| `TempsPosDébut`    | Temps de positionnement initial de la tête de lecture (ex. 10 ms)        |
| `TempsRotation`    | Temps de latence de rotation du disque (ex. 4 ms)                        |
| `TempsDépBras`     | Temps de déplacement du bras (ex. 6 ms)                                  |
| `TauxTransVrac`    | Taux de transfert en vrac (ex. 40 Mo/s)                                  |
| `TempsESBloc`      | Temps d’entrée/sortie pour un bloc (ex. 11 ms)                           |
| `TempsTrans`       | Temps de transfert d’un bloc sans repositionnement (ex. 0,1 ms)          |
| `TailleBloc`       | Taille d’un bloc disque (ex. 4 Ko)                                        |

## Structure des données

![image](https://github.com/user-attachments/assets/007949e8-f919-4558-8a35-ff1b472be49f)


### Table `Prêt`

- Nombre de tuples `N_Prêt` : 525 000  
- Facteur de blocage `FBM_Prêt` : 80  
- Cardinalité de `idMembre` : 10 000  
- Ordre maximal de l’index `Ordre_I` : 100  

### Table `Membre`

- Nombre de tuples `N_Membre` : 10 000  
- Facteur de blocage `FBM_Membre` : 80  
- Cardinalité de `idMembre` : 10 000  
- Ordre maximal de l’index `Ordre_I` : 100  

---

## Exercices

> Pour chaque question, estimer :
> - Le nombre de blocs concernés
> - Le temps théorique de calcul
> - Le temps réel approximatif

### 1. Balayage complet de la table `Prêt`

Lecture séquentielle avec un seul positionnement initial de la tête de lecture.

---

### 2. Balayage avec lecture par groupes de 20 blocs

Lecture séquentielle de la table `Prêt`, avec lecture de 20 blocs consécutifs à chaque positionnement.

---

### 3. Sélection par égalité (S=IP) sur `idMembre` (index primaire)

Index B+ primaire sur `idMembre` de `Prêt`.  
Le facteur de blocage dans les feuilles est de 2/3 de celui utilisé dans l’organisation séquentielle.  
Les prêts sont répartis uniformément entre les membres.

---

### 4. Taille de l’index primaire sur `idMembre`

Estimer la taille de l’index primaire sur `idMembre` de `Prêt`, en nombre de blocs.

---

### 5. Sélection par égalité (S=IS) avec index secondaire

Utilisation d’un index secondaire sur `idMembre` dans `Prêt`.  
Ne pas tenir compte de l’optimisation évitant la relecture de blocs.  
Ordre moyen estimé à 2/3 de l’ordre maximal.

---

### 6. Jointure `Prêt-Membre` par boucles imbriquées multi-blocs (BIM)

Deux cas :
- `Prêt` table externe
- `Membre` table externe  
Mémoire disponible : 50 blocs.

---

### 7. Jointure par boucle imbriquée avec index (BII)

Index primaire sur `idMembre` dans la table `Prêt`.

---

### 8. Jointure BII avec index secondaire optimisé

Index secondaire sur `idMembre` de `Prêt`, avec optimisation activée (évite relectures de blocs).

---

### 9. Jointure BII avec index primaire sur `Membre`

Index primaire sur `idMembre` dans `Membre`.

---

### 10. Jointure BII avec index secondaire sur `Membre`

Index secondaire sur `idMembre` dans `Membre`, avec optimisation activée.

---

### 11. Tri externe de la table `Prêt`

Tri complet de la table `Prêt` sur `idMembre` avec un tri externe en deux phases.

---

### 12. Estimation du coût d’un `GROUP BY`

Effectuer `GROUP BY idMembre` sur `Prêt`.

---

### 13. Projection avec élimination de doublons

Projection sur `idMembre` dans `Prêt`, avec suppression des doublons.

---

### 14. Intersection entre `Prêt` et `Membre`

Intersection entre les identifiants de membres dans `Prêt` et `Membre`.

---

### 15. Requête d’agrégation (`COUNT`, `SUM`)

Requête : `SELECT COUNT(*), SUM(montant)` sur `Prêt`.

---

### 16. Suppression ciblée

Suppression d’un tuple `idMembre = X`, avec ou sans index.

---

### 17. Mise à jour sans index

Mise à jour de `montant` pour tous les prêts d’un membre donné, sans index.

---

### 18. Mise à jour avec index secondaire

Même mise à jour que la question 17, avec index secondaire sur `idMembre`.

---

### 19. Insertion de 10 000 prêts

Ajout de 10 000 nouveaux prêts à la table `Prêt`, organisation séquentielle.  
Supposer qu’il reste de l’espace dans les blocs existants.

---

### 20. Reconstruction d’un index B+

Reconstruction complète d’un index B+ sur `idMembre` de `Prêt`, après chargement massif de données.

---
