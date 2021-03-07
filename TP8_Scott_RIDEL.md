
# TP8 - Introduction aux bases de données
*M2 IBIOM . 08/02/2021 . Scott RIDEL*

## Question 1
Affichez toutes les informations relatives à tous les étudiants, c’est à dire tous les attributs pour les enregistrements de la table etudiant.
```sql
SELECT *
FROM `etudiant`
```

## Question 2
Affichez les prénoms et les ages de tous les étudiants
```sql
SELECT `prenom`, `age` 
FROM `etudiant`
```

## Question 3
Affichez les prénoms et noms des trois étudiants dans l’ordre alphabétique (s’il y a plusieurs ́etudiants avec les mêmes prénoms et noms, ne les mettre qu’une seule fois.)
```sql
SELECT `prenom`, `nom` 
FROM `etudiant` 
GROUP BY `prenom`, `nom` 
ORDER BY `prenom`, `nom` 
LIMIT 3 
```

## Question 4
Afficher les différents prénoms des étudiants dans l’ordre alphabétique.
```sql
SELECT `prenom` 
FROM `etudiant` 
GROUP BY `prenom` 
ORDER BY `prenom` 
```

## Question 5
Affichez le nombre de villes différentes. Vous pourrez utiliser, par exemple, la fonction MySQL COUNT et afficherez ”Nombre de villes différentes”
```sql
SELECT COUNT(DISTINCT `ville`) 
AS "Nombre de villes différentes" 
FROM `etudiant` 
```

## Question 6
Affichez les noms des filières et les effectifs pour chacune des filières.
```sql
SELECT `filiere`, COUNT(*) 
AS "effectif" 
FROM `etudiant` 
GROUP BY `filiere`
```

## Question 7
Affichez les prénoms et noms des cinq étudiants inscrits en "L3Info" les plus jeunes.
```sql
SELECT `prenom`, `nom`
FROM `etudiant` 
WHERE `filiere` = "L3Info"
ORDER BY `age` DESC
LIMIT 5
```

## Question 8
Affichez les prénoms, noms et villes des étudiants inscrits en L3.
```sql
SELECT `prenom`, `nom`, `ville`
FROM `etudiant`
WHERE `filiere` LIKE "L3%"
```

## Question 9
Affichez les prénoms, noms et villes pour les étudiants qui sont en première année et dont
le prénom ne commence pas par un "M".
```sql
SELECT `prenom`, `nom`, `ville`
FROM `etudiant`
WHERE `filiere` LIKE "L1%"
AND `prenom` NOT LIKE "M%"
```

## Question 10
Affichez les noms et effectifs des filières ayant au moins 1850 inscrits (recherchez pour
cela la clause HAVING associée à MySQL sur internet)
```sql
SELECT `filiere`, COUNT(*)
AS "effectif" 
FROM etudiant GROUP BY `filiere` 
HAVING COUNT(*) >= 1850
```
