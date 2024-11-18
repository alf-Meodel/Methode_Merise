<a href="../README.md"><img src="../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_rt.png)

# Dailys 4 MERISE

![border](../assets/line/line-pink-point_l.png)

## Notes

```
CIF : regles de gestion bien goupillés
CIP: que les propriétés et attributs soient bien respectés
```

![border](../assets/line/border_deco_rb.png)

# MERISE - Le MLD (Modèle Logique de Données)

![border](../assets/line/line-pink-point_r.png)

## Sommaire

- [x] Passage du MCD au MLD
  - [x] [Savoir appliquer les règles de passage](#savoir-appliquer-les-règles-de-passage)
  - [x] [Savoir gérer les relations 1:1](#savoir-gérer-les-relations-11)
  - [x] [Savoir gérer les relations 1:N](#savoir-gérer-les-relations-1n)
  - [x] [Savoir gérer les relations N:M](#savoir-gérer-les-relations-n--m)
  - [x] [Savoir gérer les contraintes d'intégrité](#savoir-gérer-les-contraintes-dintégrité)
    - [x] Clés primaires
    - [x] Clés étrangères
    - [x] Contraintes d'unicité

![border](../assets/line/line-pink-point_r.png)

## Tableau recapitulatif

| **Aspect**                       | **Description**                                                                                                                         | **Exemple concret**                                                                                                           |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Entités → Tables**             | Chaque entité du MCD devient une table dans le MLD. Les attributs de l'entité deviennent les colonnes de la table.                      | L'entité "Livre" devient la table "Livre" avec les colonnes : ISBN, Titre.                                                    |
| **Relations 1:1**                | Une relation 1:1 peut être fusionnée dans une seule table ou représentée par une clé étrangère dans l'une des tables.                   | Table "Adhérent" avec les colonnes : ID Adhérent, Nom, Adresse, DateAdhésion, DateExpiration.                                 |
| **Relations 1:N**                | Une relation 1:N est représentée par l'ajout d'une clé étrangère dans la table correspondant au côté "N".                               | Table "Livre" avec la colonne ID Auteur (FK) pour lier chaque livre à un auteur.                                              |
| **Relations N:M**                | Une relation N:M est représentée par une table intermédiaire contenant des clés étrangères pour lier les deux tables.                   | Table "Suivre" avec les colonnes : ID Étudiant (FK), ID Cours (FK) pour représenter les élèves inscrits dans plusieurs cours. |
| **Clés primaires**               | Chaque table doit avoir une clé primaire unique pour identifier chaque ligne de manière distincte.                                      | Table "Auteur" avec la clé primaire : ID Auteur.                                                                              |
| **Clés étrangères**              | Les clés étrangères permettent de représenter les relations entre les tables et de garantir l'intégrité référentielle.                  | ID Auteur (FK) dans la table "Livre" pour lier chaque livre à son auteur.                                                     |
| **Contraintes d'unicité**        | Elles empêchent les doublons dans une table pour garantir l'intégrité des données.                                                      | L'ISBN dans la table "Livre" est unique pour chaque livre.                                                                    |
| **Avantages du MLD**             | Le MLD organise les données pour garantir leur intégrité, éliminer les redondances et faciliter les requêtes.                           | Une base de données structurée est plus performante, plus simple à mettre à jour et réduit les erreurs de conception.         |
| **Optimisation avec 2FN et 3FN** | Les formes normales éliminent les dépendances inutiles (partielles et transitives) pour éviter les redondances et faciliter la gestion. | PrixProduit dans la table "Produit" (2FN) et ResponsableDépartement dans une table séparée (3FN).                             |

![border](../assets/line/line-pink-point_r.png)

# Passage du MCD au MLD

### Définition

Le passage du MCD (Modèle Conceptuel de Données) au MLD (Modèle Logique de Données) consiste à convertir des entités et relations du MCD en tables et relations dans une base de données relationnelle. Ce processus suit des règles pour structurer les données efficacement.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-pink-point_r.png)

## Savoir appliquer les règles de passage

La transformation du MCD au MLD consiste à convertir chaque entité en table et chaque association en relation. Les relations 1:1, 1:N et N:M sont adaptées selon des règles spécifiques pour garantir l'intégrité et la cohérence des données.

### Explication imagée :

```
Imaginez un puzzle : chaque pièce représente une entité ou une
relation. Le passage au MLD consiste à organiser ces pièces pour
qu’elles s’assemblent parfaitement dans une base de données logique.
```

### Cas concret :

Prenons une entité "Livre" avec des attributs simples et une relation avec "Auteur".

### MCD :

- Entité Livre : ISBN, Titre.
- Entité Auteur : ID Auteur, Nom.
- Relation : Un auteur peut écrire plusieurs livres (1).

### MLD :

#### Table Livre :

| ISBN       | Titre          | ID Auteur (FK) |
| ---------- | -------------- | -------------- |
| 978-123456 | Les Misérables | 1              |
| 978-654321 | Le Hobbit      | 2              |

#### Table Auteur :

| ID Auteur | Nom         |
| --------- | ----------- |
| 1         | Victor Hugo |
| 2         | Tolkien     |

![border](../assets/line/line-pink-point_r.png)

## Savoir gérer les relations 1:1

```
Une relation 1:1 signifie qu'une occurrence dans une
entité correspond exactement à une occurrence dans
l'autre. Elle peut être représentée en fusionnant les
entités ou en utilisant une clé étrangère.
```

### Explication imagée :

Imaginez un permis de conduire : chaque conducteur a un permis unique. La relation entre le conducteur et son permis est 1:1. Dans une base de données, ces informations peuvent être stockées ensemble ou séparément selon les besoins.

### Cas concret :

Relation entre Adhérent et CarteAdhésion.

### MCD :

| Adhérent    | CarteAdhésion    |
| ----------- | ---------------- |
| ID Adhérent | ID Adhérent (FK) |
| Nom         | DateAdhésion     |
| Adresse     | DateExpiration   |

### MLD (fusion des entités) :

| ID Adhérent | Nom    | Adresse          | DateAdhésion | DateExpiration |
| ----------- | ------ | ---------------- | ------------ | -------------- |
| 1           | Dupont | 10 rue des Lilas | 01/01/2024   | 01/01/2025     |

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-pink-point_r.png)

## Savoir gérer les relations 1:N

```
Une relation 1:N relie une occurrence dans une entité à plusieurs occurrences dans une autre. Elle est représentée en ajoutant une clé étrangère dans la table correspondant à l'entité du côté "N".
```

### Explication imagée :

```
Imaginez une bibliothèque : un auteur peut écrire plusieurs livres, mais chaque livre est écrit par un seul auteur. La relation 1:N est représentée par un lien direct entre les auteurs et leurs livres.
```

## Cas concret :

### MCD :

| ID Auteur | Nom         | ISBN (FK)  | Titre          |
| --------- | ----------- | ---------- | -------------- |
| 1         | Victor Hugo | 978-123456 | Les Misérables |
| 2         | Tolkien     | 978-654321 | Le Hobbit      |

### MLD :

##### Table Auteur :

| ID Auteur | Nom         |
| --------- | ----------- |
| 1         | Victor Hugo |
| 2         | Tolkien     |

##### Table Livre :

| ISBN       | Titre          | ID Auteur (FK) |
| ---------- | -------------- | -------------- |
| 978-123456 | Les Misérables | 1              |
| 978-654321 | Le Hobbit      | 2              |

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-pink-point_r.png)

## Savoir gérer les relations N | M

Une relation N:M relie plusieurs occurrences d’une entité à plusieurs occurrences d’une autre. Elle est représentée par une table intermédiaire contenant des clés étrangères des deux entités.

## Explication imagée :

### Imaginez une classe :

plusieurs élèves suivent plusieurs cours. Plutôt que de noter tous les cours suivis par chaque élève dans une seule table, on utilise une table intermédiaire pour gérer les associations.

### Cas concret :

#### MCD :

Relation entre Étudiant et Cours.

### MLD :

- Table Étudiant :

| ID Étudiant | Nom   |
| ----------- | ----- |
| 1           | Alice |
| 2           | Bob   |

- Table Cours :

| ID Cours | Intitulé      |
| -------- | ------------- |
| 101      | Mathématiques |
| 102      | Physique      |

- Stable Suivre (relation intermédiaire) :

| ID Étudiant (FK) | ID Cours (FK) |
| ---------------- | ------------- |
| 1                | 101           |
| 1                | 102           |
| 2                | 101           |

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

# Savoir gérer les contraintes d'intégrité

```
Les contraintes d'intégrité garantissent la cohérence des données. Elles incluent les clés primaires, les clés étrangères, et les contraintes d'unicité pour éviter les doublons ou les erreurs.
```

### Explication imagée :

```
Pensez à une serrure et une clé : une clé primaire identifie chaque ligne de manière unique, et une clé étrangère établit une relation avec une autre table.
```

## Clés primaires, clés étrangères, et contraintes d'unicité

### Clés primaires

```
Chaque table doit avoir une clé primaire unique.
  Exemple : ID Auteur pour identifier chaque auteur.
```

#### Définition :

Une clé primaire est un identifiant unique pour chaque ligne d'une table. Elle garantit que chaque enregistrement peut être distingué des autres.

### Explication imagée :

```
Imaginez une carte d'identité : chaque personne a un numéro unique
qui lui est propre. Dans une table, la clé primaire joue le même
 rôle : elle permet d'identifier chaque ligne de manière unique.
```

### Cas concret :

#### Prenons la table Auteur.

### MCD :

| Entité | Attributs      |
| ------ | -------------- |
| Auteur | ID Auteur, Nom |

### MLD (avec clé primaire) :

| ID Auteur (PK) | Nom         |
| -------------- | ----------- |
| 1              | Victor Hugo |
| 2              | Tolkien     |

ID Auteur est défini comme la clé primaire (PK), car elle identifie de manière unique chaque auteur.

## Clés étrangères

```
Les relations entre tables utilisent des clés étrangères.
  Exemple : ID Auteur (FK) dans la table Livre pour lier les livres aux auteurs.
```

### Définition :

Une clé étrangère est une colonne dans une table qui pointe vers une clé primaire d'une autre table. Elle établit une relation entre les deux tables.

### Explication imagée :

Pensez à une relation parent-enfant : chaque enfant connaît son parent grâce à un lien direct. Une clé étrangère fonctionne de la même manière : elle relie une table (enfant) à une autre (parent).

#### Cas concret :

Relation entre Livre et Auteur (1).

## MCD :

| Entité Livre | Entité Auteur  |
| ------------ | -------------- |
| ISBN, Titre  | ID Auteur, Nom |

## MLD (avec clé étrangère) :

### Table Livre :

| ISBN       | Titre          | ID Auteur (FK) |
| ---------- | -------------- | -------------- |
| 978-123456 | Les Misérables | 1              |
| 978-654321 | Le Hobbit      | 2              |

### Table Auteur :

| ID Auteur (PK) | Nom         |
| -------------- | ----------- |
| 1              | Victor Hugo |
| 2              | Tolkien     |

- ID Auteur (FK) dans la table Livre fait référence à la clé primaire ID Auteur (PK) dans la table Auteur. Cela garantit que chaque livre est associé à un auteur valide.

## Contraintes d'unicité

```
 Empêcher les doublons dans une table.
  Exemple : Un ISBN ne peut apparaître qu'une seule fois dans la table Livre.
```

### Définition :

Les contraintes d'unicité empêchent les doublons dans une colonne ou une combinaison de colonnes d'une table. Cela garantit l'intégrité des données.

### Explication imagée :

```
Imaginez une bibliothèque : chaque livre a un numéro ISBN unique.
 Une contrainte d'unicité garantit qu'aucun livre ne puisse avoir
 le même ISBN dans la base de données.
```

### Cas concret :

### La table Livre avec une contrainte d'unicité sur ISBN.

#### MLD (avec contrainte d'unicité) :

| ISBN       | Titre          | ID Auteur (FK) |
| ---------- | -------------- | -------------- |
| 978-123456 | Les Misérables | 1              |
| 978-654321 | Le Hobbit      | 2              |

- ISBN est défini comme une colonne unique.
- Si un utilisateur tente d'ajouter un livre avec un ISBN déjà existant, la base de données rejettera l'opération.

## Résumé des trois étapes :

### Clés primaires :

- Chaque table doit avoir une clé primaire pour identifier chaque ligne de manière unique.
- Exemple : ID Auteur dans la table Auteur.

### Clés étrangères :

- Les relations entre les tables sont établies via des clés étrangères qui pointent vers des clés primaires.
- Exemple : ID Auteur (FK) dans la table Livre.

### Contraintes d'unicité :

- Les colonnes nécessitant des valeurs uniques (ex. ISBN) doivent être définies avec une contrainte d'unicité.
- Exemple : ISBN dans la table Livre.
  Tous les tableaux ont été convertis en Markdown. Si vous souhaitez des précisions ou des ajouts, faites-le-moi savoir !

![border](../assets/line/line-pink-point_r.png)

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_l.png)
