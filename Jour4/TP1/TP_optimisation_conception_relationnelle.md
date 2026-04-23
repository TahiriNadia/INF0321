# Travail Pratique – Conception Relationnelle Avancée et Optimisation

---

## Objectifs

À la fin de ce travail pratique, vous serez capable de :

- Analyser des schémas relationnels complexes
- Identifier et corriger des anomalies de conception
- Appliquer la normalisation jusqu’à la FNBC et la 5FN
- Décomposer une relation sans perte d’information
- Raisonner sur les dépendances fonctionnelles et multivaluées
- Interpréter des choix de conception en base de données

---

## Consignes générales

- Vous devez justifier toutes vos réponses
- Les raisonnements doivent être structurés et formels
- Les schémas doivent être clairs et cohérents
- Toute réponse non justifiée sera considérée incomplète

---

# Partie 1 – Analyse de schémas

## Question 1
Soit la relation suivante :

**Reservation(Client, Chambre, Hotel, VilleHotel, DateDebut, DateFin)**

Dépendances fonctionnelles :
- Chambre → Hotel
- Hotel → VilleHotel
- (Client, Chambre, DateDebut) → DateFin

1. Déterminez les clés candidates
2. Analysez les violations de normalisation
3. Proposez une décomposition en 3FN

---

## Question 2
Soit la relation :

**Employe(NumEmp, Nom, Projet, ChefProjet, BudgetProjet)**

Dépendances :
- NumEmp → Nom
- Projet → ChefProjet, BudgetProjet

1. Identifier les dépendances partielles et transitives
2. Normaliser jusqu’à la FNBC

---

## Question 3
Soit la relation :

**Commande(NumCommande, Client, Produits, Quantités, PrixTotal)**

1. Identifier les problèmes de conception
2. Proposer une transformation en 1FN puis en 3FN

---

# Partie 2 – Décomposition et dépendances

## Question 4
Soit R(A, B, C, D, E) avec :

- A → B
- B → C
- C → D
- D → E

1. Déterminez la clé candidate
2. Décomposez en FNBC
3. Vérifiez la conservation des dépendances

---

## Question 5
Soit la relation suivante :

R(Etudiant, Cours, Enseignant, Salle)

Dépendances :
- Cours → Enseignant
- Enseignant → Salle

1. Identifier les anomalies
2. Proposer une décomposition sans perte

---

## Question 6
Expliquez pourquoi une décomposition peut :
- être sans perte
- mais ne pas préserver les dépendances

Donnez un exemple concret.

---

# Partie 3 – Normalisation avancée (4FN et 5FN)

## Question 7
Soit la relation :

R(Auteur, Livre, MaisonEdition)

Hypothèse :
- Un auteur peut écrire plusieurs livres
- Un livre peut être publié par plusieurs maisons d’édition

1. Identifier les dépendances multivaluées
2. Proposer une décomposition en 4FN

---

## Question 8
Soit la relation :

R(Fournisseur, Pièce, Projet)

avec dépendance jointe implicite entre les trois attributs.

1. Expliquer pourquoi la 5FN est nécessaire
2. Décomposer la relation en 5FN

---

## Question 9
Donner un exemple réel (non théorique) où la 5FN est pertinente.

---

# Partie 4 – Raisonnement sur les clés

## Question 10
Soit R(A, B, C, D, E, F) avec :

- A → B
- B → C
- (A, D) → E
- E → F

1. Déterminer les clés candidates
2. Identifier les attributs non premiers
3. Proposer une décomposition FNBC

---

## Question 11
Expliquez la différence entre :
- super-clé
- clé candidate
- clé primaire

---

## Question 12
Est-il possible d’avoir plusieurs clés candidates ? Justifiez avec un exemple.

---

# Partie 5 – Cas intégrateur

## Question 13

Soit une base de données d’un système universitaire :

**Inscription(Étudiant, Cours, Enseignant, Département, Note, Salle, Horaire)**

Dépendances :
- Cours → Enseignant
- Enseignant → Département
- (Étudiant, Cours) → Note
- Cours → Salle, Horaire

1. Identifier toutes les dépendances fonctionnelles implicites
2. Déterminer la clé candidate
3. Normaliser jusqu’à la FNBC
4. Proposer un schéma final cohérent

---

## Question 14
Expliquez les risques d’un schéma non normalisé dans un système universitaire réel.

---

## Question 15
Proposez une stratégie de conception progressive :
- du modèle conceptuel
- vers un modèle relationnel en FNBC

---

# Partie 6 – Question de réflexion

## Question 16
Pensez-vous que la normalisation doit toujours être poussée jusqu’à la 5FN ?

Justifiez votre réponse en tenant compte :
- performance
- complexité
- lisibilité du modèle

---

## Question 17
Dans quels cas industriels préfère-t-on un modèle partiellement dénormalisé ?

---

## Question 18
Expliquez comment un mauvais choix de clés peut impacter :
- les performances
- l’intégrité des données

---

## Question 19
Proposez une méthode systématique pour vérifier la FNBC d’un schéma donné.

---

## Question 20
Expliquez comment vous aborderiez la conception d’une base de données à partir d’un cahier des charges incomplet.

---

## Références
- C. J. Date — *Database Design and Relational Theory*
- Elmasri & Navathe — *Fundamentals of Database Systems*
- Notes de cours : Normalisation avancée