# 📚 Solutionnaire Complet : Estimations de performances d’accès disque

## Paramètres Récapitulatif

- \( \text{TempsPosDébut} = 10\ \text{ms} \)
- \( \text{TempsRotation} = 4\ \text{ms} \)
- \( \text{TempsDépBras} = 6\ \text{ms} \)
- \( \text{TauxTransVrac} = 40\ \text{Mo/s} \)
- \( \text{TempsESBloc} = 11\ \text{ms} \)
- \( \text{TempsTrans} = 0.1\ \text{ms} \)
- \( \text{TailleBloc} = 4\ \text{Ko} \)

Tables :

- `Prêt` : \( N_{\text{Prêt}} = 525\,000 \), \( FBM_{\text{Prêt}} = 80 \)
- `Membre` : \( N_{\text{Membre}} = 10\,000 \), \( FBM_{\text{Membre}} = 80 \)
- Ordre maximal index : \( Ordre_I = 100 \)

---

# Exercice 1 : Balayage complet de la table `Prêt`

### Nombre de blocs :

$$
\text{Nb\_Blocs\_Prêt} = \left\lceil \frac{525000}{80} \right\rceil = 6563\ \text{blocs}
$$

### Temps théorique :

$$
\text{Temps théorique} = \text{TempsPosDébut} + \text{Nb\_Blocs\_Prêt} \times \text{TempsTrans}
$$

$$
= 10 + 6563 \times 0.1 = 666.3\ \text{ms}
$$

### Temps réel :

$$
\text{Temps réel} = 6563 \times 11 = 72193\ \text{ms} = 72.2\ \text{secondes}
$$

---

# Exercice 2 : Balayage par groupes de 20 blocs

### Nombre de groupes :

$$
\text{Nb\_groupes} = \left\lceil \frac{6563}{20} \right\rceil = 329
$$

### Temps théorique :

$$
\text{Temps théorique} = 329 \times (10 + 4) + 6563 \times 0.1
$$

$$
= 329 \times 14 + 656.3 = 5262.3\ \text{ms}
$$

### Temps réel :

$$
\text{Temps réel} = 6563 \times 11 = 72193\ \text{ms}
$$

---

# Exercice 3 : Sélection par égalité (S=IP) sur `idMembre`

### Calcul :

Facteur d’occupation des feuilles :

$$
\text{Facteur\_Feuille} = \frac{2}{3} \times 80 = 53.33
$$

Nombre de feuilles :

$$
\text{Nb\_Feuilles} = \frac{525000}{53.33} \approx 9842
$$

Profondeur de l’index :

$$
\text{Profondeur} \approx \log_{66}(9842) \approx 3
$$

### Temps théorique :

$$
\text{Temps théorique} = 3 \times (10 + 4 + 0.1) = 42.3\ \text{ms}
$$

---

# Exercice 4 : Taille de l'index primaire sur `idMembre`

### Calcul :

- Feuilles : \( 9842 \)
- Niveau 1 : \( \left\lceil \frac{9842}{66} \right\rceil = 149 \)
- Niveau 2 : \( \left\lceil \frac{149}{66} \right\rceil = 3 \)

### Taille totale :

$$
\text{Taille totale} = 9842 + 149 + 3 = 9994\ \text{blocs}
$$

---

# Exercice 5 : Sélection par égalité (S=IS) avec index secondaire

### Calcul :

Ordre moyen :

$$
Ordre_{\text{moyen}} = \frac{2}{3} \times 100 = 66
$$

Feuilles :

$$
\text{Nb\_Feuilles\_IS} = \frac{10000}{66} \approx 152
$$

Profondeur :

$$
\text{Profondeur} \approx \log_{66}(152) \approx 2
$$

Temps théorique :

$$
\text{Temps\_total} = (2 \times 14.1) + 14.1 = 42.3\ \text{ms}
$$

---

# Exercice 6 : Jointure `Prêt-Membre` par BIM

Mémoire disponible : 50 blocs.

## Prêt table externe

Nombre de blocs de `Membre` :

$$
\text{Nb\_Blocs\_Membre} = \left\lceil \frac{10000}{80} \right\rceil = 125
$$

Coût :

$$
\text{Coût} = \text{Nb\_Blocs\_Prêt} + \left( \frac{\text{Nb\_Blocs\_Prêt}}{50} \times \text{Nb\_Blocs\_Membre} \right)
$$

$$
= 6563 + \left( \frac{6563}{50} \times 125 \right) \approx 6563 + 16408 = 22971\ \text{blocs}
$$

---

# Exercice 7 : Jointure BII avec index primaire sur `Prêt`

Coût :

$$
\text{Coût} = \text{Nb\_Blocs\_Membre} + (\text{N\_Membre} \times \text{Profondeur index})
$$

$$
= 125 + (10000 \times 3) = 300125\ \text{blocs}
$$

---

# Exercice 8 : Jointure BII avec index secondaire optimisé

Même idée que Exercice 7 mais en évitant la relecture multiple.

Coût :

$$
\text{Coût} \approx 6563 + 125 = 6688\ \text{blocs}
$$

---

# Exercice 9 : Jointure BII avec index primaire sur `Membre`

Coût :

$$
\text{Coût} = 6563 + (525000 \times 3)
$$

$$
= 6563 + 1575000 = 1581563\ \text{blocs}
$$

---

# Exercice 10 : Jointure BII avec index secondaire sur `Membre`

Optimisation activée :

$$
\text{Coût} \approx 6563 + 125 = 6688\ \text{blocs}
$$

---

# Exercice 11 : Tri externe de la table `Prêt`

Nombre de passes pour tri externe (Mémoire de 50 blocs) :

$$
\text{Nb\_Passes} = \left\lceil \log_{49}(6563) \right\rceil
$$

Approximation :

$$
\text{Nb\_Passes} \approx 2
$$

Coût total :

$$
\text{Coût} = 2 \times 2 \times 6563 = 26252\ \text{blocs}
$$

---

# Exercice 12 : Estimation du coût d’un `GROUP BY`

Même coût qu’un tri externe :

$$
\text{Coût} = 26252\ \text{blocs}
$$

---

# Exercice 13 : Projection avec élimination de doublons

Même coût qu’un tri :

$$
\text{Coût} = 26252\ \text{blocs}
$$

---

# Exercice 14 : Intersection entre `Prêt` et `Membre`

Intersection par tri :

$$
\text{Coût total} = 2 \times (\text{Coût tri Prêt}) + 2 \times (\text{Coût tri Membre})
$$

Pour Membre :

$$
\text{Coût tri Membre} = 2 \times 125 = 250\ \text{blocs}
$$

Donc :

$$
\text{Coût total} = 2 \times 26252 + 2 \times 250 = 53004\ \text{blocs}
$$

---

# Exercice 15 : Requête d’agrégation (`COUNT`, `SUM`)

Balayage complet :

$$
\text{Coût} = 6563\ \text{blocs}
$$

---

# Exercice 16 : Suppression ciblée

## Avec index :

Temps :

$$
\text{Temps} = \text{Profondeur} \times (\text{TempsPosDébut} + \text{TempsRotation} + \text{TempsTrans}) = 42.3\ \text{ms}
$$

## Sans index :

Balayage complet :

$$
\text{Temps réel} = 72.2\ \text{secondes}
$$

---

# Exercice 17 : Mise à jour sans index

Balayage complet de `Prêt` :

$$
\text{Coût} = 6563\ \text{blocs}
$$

---

# Exercice 18 : Mise à jour avec index secondaire

Accès via l'index secondaire :

$$
\text{Coût} = 2 \times (\text{Temps\_index}) + \text{Temps\_mise\_à\_jour}
$$

---

# Exercice 19 : Insertion de 10 000 prêts

Si espace libre dans blocs existants :

Coût ≈ insertion directe :

$$
\text{Coût} \approx \frac{10000}{80} = 125\ \text{blocs}
$$

---

# Exercice 20 : Reconstruction d’un index B+

Chargement massif :

$$
\text{Coût} \approx 2 \times 6563 = 13126\ \text{blocs}
$$

---

