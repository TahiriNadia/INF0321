# TD : Approfondissement de la Conception Relationnelle

## Module : C_MOD_CO3x

### Objectifs
- Maîtriser la normalisation jusqu'à la cinquième forme normale (5FN).
- Comprendre et appliquer les concepts de première forme normale (1FN) et de forme normale de Boyce-Codd (FNBC).
- Être capable d'inférer directement un schéma relationnel à partir d'un ensemble de dépendances fonctionnelles (DF).

---

## Consignes générales
- Répondez de manière claire, précise et structurée.
- Justifiez systématiquement vos réponses par des définitions, raisonnements et exemples formels.
- Utilisez des notations formelles adaptées.
- Remettez votre travail au format PDF ou Markdown.

---

## Partie 1 : Rappels fondamentaux

### Question 1
Définir la première forme normale (1FN).  
Donner un exemple de relation qui ne satisfait pas cette forme.

### Question 2
Quels sont les problèmes potentiels lorsqu'une relation n'est pas en 1FN ?

### Question 3
Définir la forme normale de Boyce-Codd (FNBC).  
Quelle est la principale différence entre la 3FN et la FNBC ?

### Question 4
Fournir un exemple de relation respectant la 3FN mais violant la FNBC.

### Question 5
Présenter formellement la définition de la cinquième forme normale (5FN).  
Pourquoi la 5FN est-elle rarement appliquée en pratique ?

---

## Partie 2 : Applications pratiques

### Question 6
La relation suivante est-elle en 1FN ? Si non, proposer une normalisation.

**Relation Étudiant :**

| Étudiant | Matières     | Notes    |
|:--------:|:------------:|:--------:|
| Dupont   | Math, Info   | 15, 14   |
| Martin   | Info         | 12       |

---

### Question 7
Considérons la relation R(A, B, C) avec les dépendances fonctionnelles suivantes :

- A → B
- B → C

Décomposer R en un ensemble de relations satisfaisant la FNBC.

**Schéma de départ :**

| A (clé) | B | C |
|:-------:|:-:|:-:|

---

### Question 8
À partir des dépendances fonctionnelles suivantes, inférer un schéma relationnel minimal :

- CodeProduit → NomProduit, Prix
- CodeProduit, CodeMagasin → Stock

**Relations attendues :**

1. **Produit :**

| CodeProduit (PK) | NomProduit | Prix |
|:----------------:|:----------:|:----:|

2. **Stock :**

| CodeProduit (FK) | CodeMagasin (FK) | Stock |
|:----------------:|:---------------:|:-----:|

---

### Question 9
Donner un exemple concret de situation nécessitant une normalisation jusqu'à la 5FN.

---

## Partie 3 : Approfondissements théoriques

### Question 10
Qu'est-ce qu'une décomposition sans perte ? Illustrer avec un exemple.

### Question 11
Définir la dépendance multivaluée (DMV).  
Pourquoi est-elle importante pour atteindre la quatrième forme normale (4FN) ?

### Question 12
Expliquer comment déterminer une clé primaire à partir d'un ensemble de dépendances fonctionnelles.

### Question 13
Expliquer la différence entre :
- Dépendance fonctionnelle
- Dépendance fonctionnelle partielle
- Dépendance fonctionnelle transitive

Illustrer chaque notion par un exemple.

### Question 14
Considérons la relation R(U, V, W, X, Y) avec les dépendances fonctionnelles suivantes :
- U → V
- V → W
- (U, X) → Y

Déterminer tous les candidats clés de R.

**Schéma de départ :**

| U | V | W | X | Y |
|:-:|:-:|:-:|:-:|:-:|

---

## Partie 4 : Cas pratiques complexes

### Question 15
Considérons la relation suivante :

| Commande | Produit | Fournisseur | Quantité |
|:--------:|:-------:|:-----------:|:--------:|

avec les dépendances fonctionnelles :
- (Commande, Produit) → Quantité
- Produit → Fournisseur

Normaliser cette relation jusqu'à la FNBC.

---

### Question 16
Énoncer les étapes successives pour normaliser une relation jusqu'à la 5FN.

### Question 17
Un ensemble minimal de dépendances fonctionnelles est-il unique ? Justifiez votre réponse.

---

## Partie 5 : Questions ouvertes / Discussions

### Question 18
Dans quels cas la dénormalisation est-elle préférable en conception de bases de données relationnelles ? Donner un exemple concret.

### Question 19
Comparer les avantages et inconvénients :
- d'un modèle très normalisé (jusqu'à la 5FN),
- d'un modèle modérément normalisé (jusqu'à la 3FN).

### Question 20
Proposer une méthode systématique pour inférer directement un schéma relationnel respectant la FNBC à partir d'un ensemble de dépendances fonctionnelles.

---

## Ressources complémentaires
- C. J. Date, *An Introduction to Database Systems*
- Elmasri & Navathe, *Fundamentals of Database Systems*
- Notes de cours : *Normalisation avancée*, Polytechnique Montréal
