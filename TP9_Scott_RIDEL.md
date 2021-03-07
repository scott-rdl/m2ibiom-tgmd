
# TP9 - Introduction aux bases de données
*M2 IBIOM . 11/02/2021 . Scott RIDEL*

## Question 1
Combien les tables etudiantetcourscontiennent-elle d’enregistrements ?
 - etudiants : 600 entrées
 - cours : 8 entrées

## Question 2
Quelle est la clause permettant d’utiliser conjointement les entités etudiant, cours et filiere?
```sql
SELECT * FROM `etudiant`, `cours`, `filiere`, `etu_cou`
WHERE filiere.fil_id = etudiant.etu_fil_id
AND etudiant.etu_id = etu_cou.etu_id
AND cours.cou_id = etu_cou.cou_id
```

## Question 3
Il y a 600 étudiants. Les 7200 résultats indiquent que PHPMyAdmin n'a pas su associer les tables etudiant et filieres. En effet il manque les clauses d'associations
entre les tables etudiant et filieres dans cette requette.

## Question 4
Affichez les intitulés des filières et les noms des étudiants nés à Rouen appartenant à ces filières.
```sql
SELECT `fil_intitule`, `etu_nom`
FROM `etudiant` e, `filiere` f
WHERE f.fil_id = e.etu_fil_id
AND e.etu_ville LIKE "Rouen"
```

## Question 5
Affichez  les  intitulés  de  la  filière  et  le  nombre  d'étudiants  inscrits  pour  chacune  des filières pour correspondre à l’affichage ci-dessous.
```sql
SELECT `fil_intitule` "Filière", COUNT(*) "Effectif"
FROM `etudiant` e, `filiere` f
WHERE f.fil_id = e.etu_fil_id
GROUP BY fil_intitule
```

## Question 6
Affichez le nom de la filière où il y a le plus grand nombre d'étudiants inscrits.
```sql
SELECT `fil_intitule` "Filière", COUNT(*) "Effectif"
FROM `etudiant` e, `filiere` f
WHERE f.fil_id = e.etu_fil_id
GROUP BY fil_intitule
ORDER BY COUNT(*) DESC limit 1
```

## Question 7
Affichez les prénoms et noms des étudiants inscrits en cours d’Anglais.
```sql
SELECT `etu_prenom`, `etu_nom`
FROM `etudiant` e
INNER JOIN etu_cou ec ON e.etu_id = ec.etu_id
INNER JOIN cours c ON ec.cou_id = c.cou_id
WHERE  cou_intitule = "Anglais"
```

## Question 8
Affichez les intitulés des cours et les effectifs pour chacun des cours.
```sql
SELECT `cou_intitule` "Cours", COUNT(*) "Effectif"
FROM `etudiant` e
INNER JOIN etu_cou ec ON e.etu_id = ec.etu_id
INNER JOIN cours c ON ec.cou_id = c.cou_id
GROUP BY cou_intitule
```

## Question 9
Affichez les intitulés des cours ayant au moins 195  étudiants inscrits et les effectifs correspondants.
```sql
SELECT `cou_intitule` "Cours", COUNT(*) "Effectif"
FROM `etudiant` e
INNER JOIN cours c ON ec.cou_id = c.cou_id
INNER JOIN etu_cou ec ON e.etu_id = ec.etu_id
GROUP BY cou_intitule 
HAVING COUNT(*) >= 195
```

## Question 10
Affichez, pour les ́etudiants d’une filière L2, leurs prénoms et noms, ainsi que leur note en Informatique. Cet affichage sera trié suivant les noms, puis les prénoms.
```sql
SELECT `etu_prenom` "Prénom", `etu_nom` "Nom",`etu_cou_note` "Note en Informatique"
FROM `etudiant` e
INNER JOIN etu_cou ec ON e.etu_id = ec.etu_id
INNER JOIN cours c ON ec.cou_id = c.cou_id
INNER JOIN filiere f ON f.fil_id = e.etu_fil_id
WHERE cou_intitule = "Informatique"
AND fil_parcours LIKE "L2%"
ORDER BY etu_nom,etu_prenom
```

## Question 11
Affichez les noms et les villes de naissance des étudiants des filières "Bio", faisant de l'anglais et dont l'âge est compris entre 19 et 21.
```sql
SELECT `etu_ville` "Ville", `etu_nom` "Nom"
FROM `etudiant` e
INNER JOIN etu_cou ec ON e.etu_id = ec.etu_id
INNER JOIN cours c ON ec.cou_id = c.cou_id
INNER JOIN filiere f ON f.fil_id = e.etu_fil_id
WHERE fil_code LIKE "Bio%"
AND cou_intitule = "Anglais"
AND etu_age BETWEEN 19 AND 21
```
