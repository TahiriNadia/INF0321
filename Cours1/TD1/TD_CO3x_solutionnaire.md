# Solutionnaire — TD Approfondissement de la Conception Relationnelle

## Partie 1 : Rappels fondamentaux

---

### Question 1
**Définir la première forme normale (1FN). Donner un exemple.**

**Réponse** :  
Une relation est en **première forme normale (1FN)** si **toutes ses valeurs d'attribut sont atomiques** (indivisibles).  
Autrement dit, chaque cellule contient une seule valeur élémentaire, et non un ensemble ou une liste.

**Exemple de relation non conforme à la 1FN** :

| Étudiant | Matières         | Notes    |
|:--------:|:----------------:|:--------:|
| Dupont   | Math, Informatique | 15, 14 |

→ Ici, "Matières" et "Notes" contiennent plusieurs valeurs séparées par des virgules.

---

### Question 2
**Quels problèmes peuvent survenir si une relation n’est pas en 1FN ?**

**Réponse** :
- Impossibilité d’appliquer des requêtes SQL standards (SELECT, JOIN).
- Difficultés de mise à jour (Update Anomaly).
- Difficultés pour assurer l’intégrité des données.
- Risque d’incohérence et de redondance.

---

### Question 3
**Définir la FNBC. Quelle est la différence principale entre 3FN et FNBC ?**

**Réponse** :  
La **forme normale de Boyce-Codd (FNBC)** exige que pour toute dépendance fonctionnelle non triviale X → Y, **X soit une super-clé**.

**Différence principale** :
- En **3FN**, il est permis qu’une dépendance existe si Y est un attribut premier (partie d’une clé).
- En **FNBC**, même ce cas est interdit : seule une super-clé peut déterminer un autre attribut.

---

### Question 4
**Donner un exemple d’une relation en 3FN mais pas en FNBC.**

**Réponse** :  
Relation `R(Étudiant, Matière, Professeur)` avec DF :
- (Étudiant, Matière) → Professeur
- Professeur → Matière

**Analyse** :
- 3FN est respectée (Matière est un attribut premier car il dépend d'une clé candidate).
- FNBC n'est pas respectée (Professeur n'est pas une super-clé).

---

### Question 5
**Définir la 5FN. Pourquoi est-elle rarement appliquée en pratique ?**

**Réponse** :  
La **cinquième forme normale (5FN)** impose que **toute décomposition** soit fondée sur une **dépendance de jointure**, garantissant une **recomposition sans perte**.

**Peu appliquée car** :
- Les cas pratiques nécessitant la 5FN sont très rares.
- L'application de la 5FN complexifie considérablement la structure des bases.
- Les coûts de jointure deviennent élevés pour peu de bénéfices.

---

## Partie 2 : Applications pratiques

---

### Question 6
**La relation suivante est-elle en 1FN ?**

| Étudiant | Matières         | Notes    |
|:--------:|:----------------:|:--------:|
| Dupont   | Math, Informatique | 15, 14 |

**Réponse** :  
Non, elle n'est pas en 1FN car "Matières" et "Notes" contiennent des ensembles.

**Normalisation correcte** :

| Étudiant | Matière        | Note |
|:--------:|:--------------:|:----:|
| Dupont   | Math           | 15   |
| Dupont   | Informatique   | 14   |

---

### Question 7
**Décomposer R(A, B, C) avec DF : A → B et B → C en FNBC.**

**Réponse** :
1. Dépendances fonctionnelles :
   - A → B
   - B → C

2. Décomposition :
   - R1(A, B)
   - R2(B, C)

**Vérifications** :
- R1 : A est clé pour B (ok)
- R2 : B est clé pour C (ok)
- Décomposition est **sans perte** et **conserve les dépendances**.

---

### Question 8
**Inférer un schéma relationnel minimal à partir des DF.**

**DF données** :
- CodeProduit → NomProduit, Prix
- CodeProduit, CodeMagasin → Stock

**Relations construites** :

- **Produit** :

| CodeProduit (PK) | NomProduit | Prix |
|:----------------:|:----------:|:----:|

- **Stock** :

| CodeProduit (FK) | CodeMagasin (FK) | Stock |
|:----------------:|:---------------:|:-----:|

---

### Question 9
**Donner un exemple concret nécessitant la 5FN.**

**Réponse** :  
Gestion de tournages de films :  
- Acteurs, Films, Rôles.

Chaque acteur peut jouer plusieurs rôles dans plusieurs films. La dépendance entre Acteur, Film et Rôle nécessite une décomposition en 5FN.

---

## Partie 3 : Approfondissements théoriques

---

### Question 10
**Définir une décomposition sans perte.**

**Réponse** :  
Une décomposition est **sans perte** si la **jointure naturelle** des relations décomposées **restitue** exactement la relation d'origine, sans introduction de tuples parasites.

**Exemple** :
Relation R(A, B, C) avec A → B.
Décomposition :
- R1(A, B)
- R2(A, C)

La jointure sur A reconstitue totalement R.

---

### Question 11
**Qu'est-ce qu'une dépendance multivaluée (DMV) ?**

**Réponse** :  
Une **dépendance multivaluée** X ↠ Y signifie que pour une valeur de X, il existe indépendamment plusieurs valeurs de Y.

**Importance** :
- Permet d'atteindre la 4FN.
- Évite la redondance et anomalies dans les bases de données complexes.

---

### Question 12
**Comment déterminer une clé primaire à partir des DF ?**

**Réponse** :
- Chercher un ensemble d'attributs minimal qui détermine tous les autres attributs.
- Tester l'atteignabilité via la fermeture (X⁺).

---

### Question 13
**Différencier dépendance fonctionnelle, partielle et transitive.**

| Type                         | Définition                                               | Exemple             |
|:-----------------------------:|:--------------------------------------------------------:|:-------------------:|
| Dépendance fonctionnelle       | X → Y : une valeur de X détermine une unique valeur de Y | Étudiant → Adresse  |
| Dépendance fonctionnelle partielle | Une partie seulement de la clé détermine Y | (Numéro Étudiant) → Nom |
| Dépendance fonctionnelle transitive | X → Z via X → Y et Y → Z | Étudiant → Groupe → Local |

---

### Question 14
**Déterminer toutes les clés candidates pour R(U, V, W, X, Y).**

**DF données** :
- U → V
- V → W
- (U, X) → Y

**Analyse** :
- U détermine V, donc W (via transitivité).
- (U, X) détermine Y.

**Clé candidate** : (U, X)

---

## Partie 4 : Cas pratiques complexes

---

### Question 15
**Normaliser la relation (Commande, Produit, Fournisseur, Quantité) jusqu'à la FNBC.**

**DF données** :
- (Commande, Produit) → Quantité
- Produit → Fournisseur

**Étapes** :
1. Décomposer selon Produit → Fournisseur :

- **Produit**(Produit, Fournisseur)

2. Ensuite :

- **CommandeProduit**(Commande, Produit, Quantité)

**Résultat** :

| Produit (PK) | Fournisseur |
|:------------:|:-----------:|

| Commande (PK) | Produit (FK) | Quantité |
|:-------------:|:------------:|:--------:|

---

### Question 16
**Énoncer les étapes pour normaliser jusqu'à la 5FN.**

**Réponse** :
1. Eliminer violations de la 1FN (atomisation).
2. Appliquer la 2FN (élimination dépendances partielles).
3. Appliquer la 3FN (élimination dépendances transitives).
4. Passer en FNBC (seulement super-clé → attribut).
5. Appliquer 4FN (traiter les DMV).
6. Appliquer 5FN (dépendances de jointure uniquement).

---

### Question 17
**Un ensemble minimal de DF est-il unique ?**

**Réponse** :  
Non. Plusieurs ensembles minimaux équivalents peuvent exister (différents choix d'attributs décomposés).

---

## Partie 5 : Questions ouvertes

---

### Question 18
**Quand préférer la dénormalisation ?**

**Réponse** :  
- Bases très volumineuses nécessitant des lectures rapides.
- Besoin de minimiser le nombre de jointures coûteuses.
- Exemple : systèmes OLAP pour reporting.

---

### Question 19
**Avantages / Inconvénients d'un modèle très normalisé vs modérément normalisé.**

| Aspect           | Très normalisé             | Modérément normalisé           |
|:----------------:|:---------------------------:|:------------------------------:|
| Intégrité        | Maximale                     | Bonne mais avec risques mineurs |
| Performances     | Moins bonnes (plus de jointures) | Meilleures (moins de jointures) |
| Maintenance      | Complexe                     | Plus simple                    |

---

### Question 20
**Proposer une méthode pour inférer directement un schéma relationnel en FNBC.**

**Réponse** :
1. Trouver les DF minimales (épuration).
2. Décomposer la relation pour chaque DF violant la FNBC.
3. S'assurer que chaque dépendance respecte la règle : antécédent = super-clé.

---
