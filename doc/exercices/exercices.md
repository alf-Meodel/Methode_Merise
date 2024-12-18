<a href="../../README.md">
  <img src="../../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;">
</a>
<a href="../dailys_3.md">
  <img src="../../assets/button/previous_page.png" alt="Back to top" style="width: 150px; height: auto;">
</a>

![border](../../assets/line/border_deco_rt.png)

# Exercices 1FN , 2FN, 3FN

![border](../../assets/line/line-pink-point_l.png)

### Sommaire

-[]()

![border](../../assets/line/border_deco_rt.png)

![border](../../assets/line/line-pink-point_l.png)

# Exercice 1 :

![border](../../assets/line/line-pink-point_l.png)

Comprendre les différentes formes normales (1FN, 2FN, 3FN)

## Comprendre la 1ère Forme Normale (1FN)

### Table initiale (non normalisée) :

| ID Commande | Client | Produits      | Quantité | Adresse Client       |
| ----------- | ------ | ------------- | -------- | -------------------- |
| 1           | Alice  | T-shirt, Jean | 2, 1     | 10 rue des Lilas     |
| 2           | Bob    | Casquette     | 3        | 20 avenue des Champs |

#### Instructions :

Identifiez les colonnes qui ne respectent pas la 1FN.
Normalisez la table pour respecter la 1FN.

## Comprendre la 2ème Forme Normale (2FN)

### Table initiale (1FN appliquée) :

| ID Commande | Client | Produit   | Quantité | Adresse Client       |
| ----------- | ------ | --------- | -------- | -------------------- |
| 1           | Alice  | T-shirt   | 2        | 10 rue des Lilas     |
| 1           | Alice  | Jean      | 1        | 10 rue des Lilas     |
| 2           | Bob    | Casquette | 3        | 20 avenue des Champs |

### Instructions :

Identifiez les colonnes avec des dépendances partielles.
Normalisez la table pour respecter la 2FN en décomposant en plusieurs tables.

### Comprendre la 3ème Forme Normale (3FN)

Table initiale (2FN appliquée) :

| ID Commande | ID Client | ID Produit | Quantité | Prix Unitaire | Adresse Client       |
| ----------- | --------- | ---------- | -------- | ------------- | -------------------- |
| 1           | 1         | 1          | 2        | 10            | 10 rue des Lilas     |
| 1           | 1         | 2          | 1        | 30            | 10 rue des Lilas     |
| 2           | 2         | 3          | 3        | 5             | 20 avenue des Champs |

### Instructions :

Identifiez les colonnes avec des dépendances transitives.
Normalisez la table pour respecter la 3FN en décomposant les dépendances transitives.

![border](../../assets/line/line-pink-point_l.png)

# Exercice 2 :

![border](../../assets/line/line-pink-point_l.png)

Identifier les dépendances fonctionnelles (DF) 4. Dépendances élémentaires

### Table :

| ÉtudiantID | Nom   |
| ---------- | ----- |
| 1          | Alice |
| 2          | Bob   |
| 3          | Carol |

### Instructions :

Identifiez la dépendance fonctionnelle élémentaire.
Expliquez pourquoi cette dépendance est élémentaire. 5. Dépendances composées

### Table :

| ÉtudiantID | CoursID | Note |
| ---------- | ------- | ---- |
| 1          | 101     | 15   |
| 1          | 102     | 18   |
| 2          | 101     | 12   |
| 3          | 103     | 14   |

### Instructions :

Identifiez la dépendance fonctionnelle composée.
Justifiez pourquoi cette dépendance nécessite plusieurs colonnes pour être définie. 6. Dépendances transitives
Table :

| EmployéID | Département  | ResponsableDépartement |
| --------- | ------------ | ---------------------- |
| 1         | Informatique | Alice                  |
| 2         | RH           | Bob                    |
| 3         | Informatique | Alice                  |

### Instructions :

Identifiez la dépendance transitive.
Expliquez comment cette dépendance fonctionne via un attribut intermédiaire.

![border](../../assets/line/line-pink-point_l.png)

# Exercice 3 :

![border](../../assets/line/line-pink-point_l.png)

Construire et valider des graphes de dépendances 7. Construire un graphe des dépendances

### Table :

| ProduitID | Catégorie    | ResponsableCatégorie |
| --------- | ------------ | -------------------- |
| 1         | Vêtements    | Alice                |
| 2         | Électronique | Bob                  |
| 3         | Vêtements    | Alice                |

### Instructions :

Construisez un graphe pour représenter les dépendances entre ProduitID, Catégorie, et ResponsableCatégorie. 8. Valider un graphe des dépendances

### Table :

| FactureID | Client | AdresseClient        |
| --------- | ------ | -------------------- |
| 1         | Alice  | 10 rue des Lilas     |
| 2         | Bob    | 20 avenue des Champs |
| 3         | Carol  | 30 avenue de la Lune |

### Instructions :

Vérifiez que toutes les flèches du graphe mènent correctement aux dépendances logiques.
Expliquez comment valider les relations entre les colonnes dans ce graphe.

### Résultats attendus

Rédigez vos réponses pour chaque exercice. Vous pouvez inclure les tables normalisées, les dépendances identifiées, et les graphes dessinés à la main ou en utilisant un outil de diagramme.

Voici la version complète en Markdown, prête à être intégrée dans votre documentation ou projet. Si vous avez besoin de modifications ou d'autres ajustements, n'hésitez pas !

![border](../../assets/line/line-pink-point_r.png)

<a href="#sommaire">
  <img src="../../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;">
</a>
<a href="/README.md">
  <img src="../../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;">
</a>

![border](../../assets/line/border_deco_l.png)
