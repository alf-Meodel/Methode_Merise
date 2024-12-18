 <a href="../README.md">
  <img src="../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_rt.png)

# Dailys 3 MERISE

![border](../assets/line/line-pink-point_l.png)

## Notes

```
(1FN) : Assure que chaque valeur dans une cellule est atomique.
(2FN) : Élimine les dépendances partielles (chaque colonne non-clé dépend complètement de la clé primaire).
(3FN) : Élimine les dépendances transitives entre les colonnes non-clés.
```

![border](../assets/line/border_deco_rb.png)

# Normalisation et dépendances fonctionnelles

## Sommaire

![border](../assets/line/line-pink-point_r.png)

- [x] [Introduction à la normalisation](#introduction-à-la-normalisation)

  - [x] Comprendre l'importance de la normalisation
  - [x] Savoir identifier les anomalies de redondance

- [x] [Les formes normales](#les-formes-normales)

  - [x] Comprendre la 1ère forme normale (1FN)
  - [x] Comprendre la 2ème forme normale (2FN)
  - [x] Comprendre la 3ème forme normale (3FN)

- [x] [Les dépendances fonctionnelles](#dépendances-fonctionnelles)

  - [x] Savoir identifier les DF élémentaires
  - [x] Savoir identifier les DF composées
  - [x] Savoir identifier les DF transitives

![border](../assets/line/line-pink-point_l.png)

## Navigation

- [Lien vers le repo de Hachemi](https://github.com/HachemiH/formation-cda-bdd)
- [Exercices](../doc/exercices/exercices.md)

# Tableau recapitulatif

| **Type**                                    | **Explication imagée**                               | **Cas concret**                                                                                   |
| ------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Comprendre l'importance de la normalisation | "Une bibliothèque bien classée."                     | Réorganiser une base de données pour éliminer les doublons et rendre les informations cohérentes. |
| Identifier les anomalies de redondance      | "Deux fiches pour un même client."                   | Une adresse client répétée dans plusieurs commandes peut causer des incohérences si elle change.  |
| Comprendre la 1ère forme normale (1FN)      | "Une boîte contient un seul type d'éléments."        | Une colonne "Téléphones" doit être atomique, sans contenir plusieurs valeurs comme "06, 07".      |
| Comprendre la 2ème forme normale (2FN)      | "Un cahier d'élèves n'a qu'une liste par page."      | Dans une table "Commandes", "PrixProduit" dépend uniquement de "ProduitID", pas de la commande.   |
| Comprendre la 3ème forme normale (3FN)      | "Un arbre sans branches inutiles."                   | "ResponsableDépartement" dépend de "Département", pas directement de "EmployéID".                 |
| Identifier les DF élémentaires              | "Une clé ouvre une serrure."                         | "Nom" dépend directement de "ÉtudiantID" dans une table "Étudiants".                              |
| Identifier les DF composées                 | "Deux clés ouvrent une boîte."                       | "Note" dépend de "ÉtudiantID" et "CoursID" dans une table "Notes".                                |
| Identifier les DF transitives               | "Une clé ouvre une boîte qui en contient une autre." | "ResponsableDépartement" dépend de "Département", qui dépend de "EmployéID".                      |
| Construire un graphe des dépendances        | "Un schéma d'organisation d'entreprise."             | Dans une table "Produits", le graphe montre que "Catégorie" dépend de "ProduitID".                |
| Valider un graphe des dépendances           | "Vérifiez que les flèches mènent au bon endroit."    | Valider une table "Factures" : "AdresseClient" dépend de "Client", qui dépend de "FactureID".     |

![border](../assets/line/border_deco_l.png)

# Introduction à la normalisation

## Comprendre l'importance de la normalisation

```
Éliminer les redondances de données.
Réduire les anomalies (de mise à jour, d'insertion, de suppression).
Améliorer la cohérence et l’intégrité des données.
```

### Explication imagée :

"Imagine une bibliothèque où les livres sont mal classés et doublés." La normalisation organise les données pour éliminer les redondances et améliorer leur cohérence.

### Cas concret :

Dans une base d'école, chaque classe possède une liste d'étudiants. Si le même étudiant est inscrit dans plusieurs classes avec des doublons de données personnelles, cela cause des erreurs et du gaspillage d'espace. La normalisation élimine ces doublons en séparant les informations des étudiants et des classes dans des tables liées.

## Savoir identifier les anomalies de redondance

```
Si je repère une redondance, je dois m'assurer qu'elle peut être éliminée en décomposant les données sans perdre d'information
```

### Explication imagée :

"Deux fiches pour le même client avec des adresses différentes." Les anomalies de redondance entraînent des erreurs lors de l'ajout, de la suppression ou de la mise à jour de données.

### Cas concret :

Dans une base de gestion de commandes, si l'adresse d’un client est stockée dans chaque commande, toute modification de l’adresse nécessite la mise à jour de toutes les commandes. Sinon, des incohérences apparaissent. La normalisation permet de déplacer l’adresse dans une table séparée "Clients".

## Définition

La normalisation est le processus qui permet d’organiser les données dans une base pour éviter la duplication, améliorer l’efficacité et garantir la cohérence des informations.

Elle permet de réduire les risques d’erreurs et de faciliter les mises à jour et la maintenance des données.

## Rien ne vaut un Bon exemple

## Table Problématique (Avant Normalisation)

| **ID Emprunt** | **Nom du Client** | **Livre**               | **Date Emprunt** | **Date Retour** | **Adresse Client**      |
| -------------- | ----------------- | ----------------------- | ---------------- | --------------- | ----------------------- |
| 1              | Alice             | Harry Potter            | 01/11/2024       | 15/11/2024      | 10 rue des Lilas        |
| 2              | Bob               | Le Hobbit               | 03/11/2024       | 17/11/2024      | 20 avenue des Champs    |
| 3              | Alice             | Le Seigneur des Anneaux | 05/11/2024       | 19/11/2024      | 10 rue des Lilas        |
| 4              | Carol             | Harry Potter            | 07/11/2024       | 21/11/2024      | 30 boulevard de la Lune |

## Problèmes de cette table

### Redondance :

- Le nom de Alice apparaît deux fois, avec la même adresse 10 rue des Lilas pour chaque emprunt.
- Le livre "Harry Potter" apparaît deux fois pour deux personnes différentes (Alice et Carol).
  Difficulté de mise à jour :

- Si Alice déménage et change d'adresse, tu devras modifier son adresse à chaque ligne où elle apparaît, ce qui peut entraîner des erreurs si tu oublies une ligne.

### Difficulté de gestion des données :

- Si un livre comme "Harry Potter" est emprunté par plusieurs personnes, tu as des informations répétées à chaque emprunt, ce qui occupe plus de place et rend la base difficile à maintenir.

---

## Attaque Normalisation !!!

Pour corriger ces problèmes, on va normaliser la base de données. Voici ce qu’on va faire :

- Séparer les informations en différentes tables pour éviter la redondance.
- Associer les informations de manière logique pour qu’on puisse les retrouver facilement sans duplication.

#### Table 1 : Clients (Après Normalisation)

| **ID Client** | **Nom** | **Adresse**             |
| ------------- | ------- | ----------------------- |
| 1             | Alice   | 10 rue des Lilas        |
| 2             | Bob     | 20 avenue des Champs    |
| 3             | Carol   | 30 boulevard de la Lune |

---

#### Table 2 : Livres (Après Normalisation)

| **ID Livre** | **Titre**               |
| ------------ | ----------------------- |
| 1            | Harry Potter            |
| 2            | Le Hobbit               |
| 3            | Le Seigneur des Anneaux |

---

#### Table 3 : Emprunts (Après Normalisation)

| **ID Emprunt** | **ID Client** | **ID Livre** | **Date Emprunt** | **Date Retour** |
| -------------- | ------------- | ------------ | ---------------- | --------------- |
| 1              | 1             | 1            | 01/11/2024       | 15/11/2024      |
| 2              | 2             | 2            | 03/11/2024       | 17/11/2024      |
| 3              | 1             | 3            | 05/11/2024       | 19/11/2024      |
| 4              | 3             | 1            | 07/11/2024       | 21/11/2024      |

---

## Avantages après la normalisation :

### Réduction de la redondance :

L’adresse de Alice n’apparaît qu’une seule fois dans la table Clients.
Le titre du livre "Harry Potter" apparaît uniquement dans la table Livres, et non plus plusieurs fois dans la table des emprunts.

### Facilité de mise à jour :

Si Alice change d’adresse, il suffit de la mettre à jour dans une seule ligne de la table Clients. Pas besoin de modifier plusieurs lignes dans la table des emprunts.

### Gestion plus simple :

Les informations sont organisées. Si tu veux savoir quels livres Alice a empruntés, tu peux consulter la table Emprunts en liant l’ID Client à la table Clients et l’ID Livre à la table Livres. C’est beaucoup plus simple à gérer et à mettre à jour.

### Conclusion Définition
La normalisation permet d’organiser les données de manière plus logique et efficace. Grâce à cela, tu évites de répéter des informations, tu réduis les erreurs possibles et tu facilites les mises à jour. C’est un peu comme ranger tes jouets dans des boîtes distinctes pour ne pas avoir un bazar dans ta chambre !

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_l.png)

# Les Formes Normales

![border](../assets/line/line-teal-point_r.png)

## Comprendre la 1ère forme normale (1FN)

```
Si je valide la 1FN, je dois m'assurer que chaque colonne contient une valeur atomique (pas de liste ou tableau dans une cellule).

pas de nom prenom dans un meme champ
```

### Explication imagée :

"Une boîte de rangement ne contient qu'un seul type d'éléments." La 1FN impose que chaque colonne ait des valeurs atomiques (non divisibles).

### Cas concret :

Une table contenant une colonne "Téléphones" avec des valeurs comme "06-12-34-56-78, 07-98-76-54-32" viole la 1FN. La 1FN exige une nouvelle ligne pour chaque numéro de téléphone, rendant les données plus exploitables et cohérentes.

![border](../assets/line/line-teal-point_r.png)

## Table non normalisée (avant d’appliquer les formes normales) :

| **ID Commande** | **Client** | **Produit** | **Quantité** | **Prix Unitaire** | **Adresse Client**   |
| --------------- | ---------- | ----------- | ------------ | ----------------- | -------------------- |
| 1               | Alice      | T-shirt     | 2            | 10                | 10 rue des Lilas     |
| 1               | Alice      | Jean        | 1            | 30                | 10 rue des Lilas     |
| 2               | Bob        | Casquette   | 3            | 5                 | 20 avenue des Champs |
| 3               | Alice      | T-shirt     | 1            | 10                | 10 rue des Lilas     |

---

##### Une table est en 1ère forme normale (1FN) si elle respecte ces conditions :

- Pas de colonnes répétées : Chaque champ doit contenir une seule valeur (c’est-à-dire, pas de listes ou de groupes de valeurs dans une colonne).
- Toutes les valeurs doivent être atomiques : Chaque cellule doit contenir une seule valeur et non un groupe de valeurs.

##### Problème avec la table actuelle :

- La table ci-dessus respecte déjà la 1ère forme car chaque colonne contient des valeurs atomiques (pas de listes ou groupes dans les cellules).
- Les données sont bien organisées en colonnes simples.

## Table en 1ère forme normale (1FN)

| **ID Commande** | **Client** | **Produit** | **Quantité** | **Prix Unitaire** | **Adresse Client**   |
| --------------- | ---------- | ----------- | ------------ | ----------------- | -------------------- |
| 1               | Alice      | T-shirt     | 2            | 10                | 10 rue des Lilas     |
| 1               | Alice      | Jean        | 1            | 30                | 10 rue des Lilas     |
| 2               | Bob        | Casquette   | 3            | 5                 | 20 avenue des Champs |
| 3               | Alice      | T-shirt     | 1            | 10                | 10 rue des Lilas     |

---

##### À ce stade, nous sommes en 1FN :
chaque cellule contient une seule valeur, et chaque ligne est une combinaison unique d’informations.

---

![border](../assets/line/line-pink-point_r.png)

## Comprendre la 2ème forme normale (2FN)

![border](../assets/line/line-pink-point_r.png)

```
Si je valide la 2FN, je dois m'assurer qu'il n'y a aucune dépendance
partielle entre les attributs d'une table et sa clé primaire.
```

```
a: dans la table etudiant on ne doit pas
retrouver des informations sur la classe ,
nom de la classe des professeurs etc...
```

### Définition :

##### Une table est en 2ème forme normale (2FN) si :

- La 2FN consiste à séparer les données pour que chaque
  colonne non-clé dépende entièrement de la clé primaire.
- Si une colonne ne dépend que d’une partie de la clé
  primaire, elle doit être déplacée dans une table à part.

### Explication imagée :

" Imagine un cahier de classe où chaque page contient deux sections : une pour les élèves et une pour les professeurs. Ce mélange rend les pages confuses et difficiles à utiliser.
En appliquant la 2FN, on sépare ces informations dans deux cahiers distincts : un pour les élèves, un pour les professeurs. Chaque cahier contient des informations claires et spécifiques. "

### Cas concret :

Prenons une table "Commandes" avec une clé primaire composée de deux colonnes : CommandeID et ProduitID.

| CommandeID | ProduitID | PrixProduit | Quantité |
| ---------- | --------- | ----------- | -------- |
| 1          | 101       | 20          | 2        |
| 1          | 102       | 15          | 1        |
| 2          | 101       | 20          | 3        |

#### Problème :
La colonne PrixProduit dépend uniquement de ProduitID, pas de la combinaison complète (CommandeID + ProduitID). Cela viole la 2FN.

#### Solution :

PrixProduit doit être déplacé dans une table séparée liée uniquement par ProduitID.

---

## Problèmes dans la table actuelle :

L’adresse du client dépend uniquement du client, pas de la commande. Cela crée une dépendance partielle.
Répéter l'adresse du client dans chaque ligne de commande est source de redondance et de risques d’erreurs.

## Solution pour passer à la 2FN :

Séparer les informations sur les clients dans une table dédiée.
Créer une table spécifique pour les commandes, avec uniquement les informations liées à chaque commande.
Créer une table pour les produits, avec leurs prix et autres détails.

![border](../assets/line/line-pink-point_l.png)

## Tables après normalisation (2FN)

#### Table Clients (après 2ème forme normale - 2FN)

| **ID Client** | **Client** | **Adresse Client**   |
| ------------- | ---------- | -------------------- |
| 1             | Alice      | 10 rue des Lilas     |
| 2             | Bob        | 20 avenue des Champs |

---

## Table Commandes (après 2ème forme normale - 2FN)

| **ID Commande** | **ID Client** | **Produit** | **Quantité** | **Prix Unitaire** |
| --------------- | ------------- | ----------- | ------------ | ----------------- |
| 1               | 1             | T-shirt     | 2            | 10                |
| 1               | 1             | Jean        | 1            | 30                |
| 2               | 2             | Casquette   | 3            | 5                 |
| 3               | 1             | T-shirt     | 1            | 10                |

---

## Table Produits (après 2ème forme normale - 2FN)

| **Produit** | **Prix Unitaire** |
| ----------- | ----------------- |
| T-shirt     | 10                |
| Jean        | 30                |
| Casquette   | 5                 |

![border](../assets/line/line-pink-point_l.png)

### Avantages de la 2FN :

### Suppression de la redondance :

- L’adresse du client est maintenant séparée dans une table Clients.
- Si Alice déménage, on n’a plus besoin de mettre à jour chaque ligne de commande, juste la ligne correspondante dans la table des Clients.

---

![border](../assets/line/line-pink-point_l.png)

## Comprendre la 3ème forme normale (3FN)

![border](../assets/line/line-teal-point_r.png)

```
La 3FN consiste à éliminer les dépendances transitives
pour que chaque colonne non-clé soit directement liée à la clé primaire.

Si une colonne non-clé dépend d’une autre colonne non-clé,
elle doit être déplacée dans une table distincte.
```

### Explication imagée :

```
Imaginez un arbre généalogique :
Dans un arbre bien structuré, chaque personne est directement reliée à ses parents. Pas besoin de branches inutiles ou de liens indirects compliqués.
La 3FN élimine ces branches inutiles, en supprimant les relations transitives.
```

```
"Imaginez un cahier d’inventaire pour un magasin. Chaque produit a son prix noté directement dans le cahier des produits, pas dans le cahier des commandes. Cela évite de répéter les prix dans chaque commande et rend les informations plus claires."
```

### Cas concret :

Prenons une table "Employés" avec les colonnes EmployéID, Département, et ResponsableDépartement :

| EmployéID | Département  | ResponsableDépartement |
| --------- | ------------ | ---------------------- |
| 1         | Informatique | Alice                  |
| 2         | RH           | Bob                    |
| 3         | Informatique | Alice                  |

---

### Problème :

ResponsableDépartement dépend de Département (et non directement de EmployéID).
Cela crée une dépendance transitive : EmployéID → Département → ResponsableDépartement.

### Solution :
Déplacer Département et ResponsableDépartement dans une table séparée.

### Définition

Une table est en 3ème forme normale (3FN) si :

Elle respecte déjà la 2ème forme normale (2FN).
Aucune colonne non-clé ne dépend d’une autre colonne non-clé via la clé primaire (dépendance transitive).
En résumé : Les colonnes non-clés doivent dépendre directement de la clé primaire et uniquement d'elle.

Problèmes dans la table actuelle (en 2FN)
Dans une table de commandes :

| ID Commande | Produit   | Prix Unitaire | Quantité |
| ----------- | --------- | ------------- | -------- |
| 1           | T-shirt   | 10            | 2        |
| 1           | Jean      | 30            | 1        |
| 2           | Casquette | 5             | 3        |

Problème :
Prix Unitaire dépend de Produit, pas directement de ID Commande.
Cela viole la 3FN, car Prix Unitaire est lié transitivement à ID Commande via Produit.
Solution pour passer à la 3FN
Séparer les informations sur les produits dans une table dédiée.
Prix Unitaire doit être enregistré dans une table indépendante liée par Produit.

## Tables après normalisation (3FN)

### Table Commandes

| ID Commande | ID Client | ID Produit | Quantité |
| ----------- | --------- | ---------- | -------- |
| 1           | 1         | 1          | 2        |
| 1           | 1         | 2          | 1        |
| 2           | 2         | 3          | 3        |
| 3           | 1         | 1          | 1        |

### Table Produits

| ID Produit | Produit   | Prix Unitaire |
| ---------- | --------- | ------------- |
| 1          | T-shirt   | 10            |
| 2          | Jean      | 30            |
| 3          | Casquette | 5             |

### Table Clients (inchangée)

| ID Client | Client | Adresse Client       |
| --------- | ------ | -------------------- |
| 1         | Alice  | 10 rue des Lilas     |
| 2         | Bob    | 20 avenue des Champs |

### Avantages de la 3FN

### Suppression des dépendances transitives :

Les informations sur les prix sont désormais gérées dans une table dédiée (Produits).
Chaque table contient uniquement des données qui dépendent directement de sa clé primaire.
Organisation simplifiée :

Les relations entre les données sont plus claires.
La gestion et les mises à jour deviennent plus faciles et moins sujettes aux erreurs.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_l.png)

# Dépendances Fonctionnelles

## Savoir identifier les DF élémentaires

```
Si j'identifie une dépendance fonctionnelle élémentaire, je dois m'assurer qu'un attribut dépend uniquement d'une autre colonne.
```

### Explication imagée :

"Une clé ouvre une seule serrure." Une DF élémentaire relie une colonne à une autre de manière directe.

### Cas concret :

| **ÉtudiantID** | **Nom** |
| -------------- | ------- |
| 1              | Alice   |
| 2              | Bob     |
| 3              | Carol   |

Dans cette table "Étudiants", "Nom" dépend directement de "ÉtudiantID". Cela signifie que chaque "ÉtudiantID" détermine un seul "Nom". Chaque étudiant a un identifiant unique qui sert à retrouver son nom sans ambiguïté. C'est une DF élémentaire.

## Savoir identifier les DF composées

```
Si j'identifie une dépendance fonctionnelle composée, je dois vérifier qu'elle implique plusieurs attributs pour déterminer une valeur.
```

### Explication imagée :

"Deux clés nécessaires pour ouvrir une boîte." Une DF composée implique plusieurs colonnes dans la détermination d’une valeur.

### Cas concret :

| **ÉtudiantID** | **CoursID** | **Note** |
| -------------- | ----------- | -------- |
| 1              | 101         | 15       |
| 1              | 102         | 18       |
| 2              | 101         | 12       |
| 3              | 103         | 14       |

Dans cette table "Notes", la DF "Note" dépend de la combinaison "ÉtudiantID" et "CoursID". Aucune de ces colonnes seules ne permet de déterminer la "Note". Par exemple, l’étudiant 1 dans le cours 101 a une note de 15, mais dans le cours 102, il a une note différente de 18. C’est une DF composée.

## Savoir identifier les DF transitives

```
Si j'identifie une dépendance fonctionnelle transitive, je dois m'assurer qu'un attribut dépend indirectement de la clé primaire via un autre attribut.
```

### Explication imagée :

"Une clé ouvre une boîte qui en contient une autre." Une DF transitive relie deux colonnes via une colonne intermédiaire.

### Cas concret :

| **EmployéID** | **Département** | **ResponsableDépartement** |
| ------------- | --------------- | -------------------------- |
| 1             | Informatique    | Alice                      |
| 2             | RH              | Bob                        |
| 3             | Informatique    | Alice                      |

Dans cette table "Employés", "ResponsableDépartement" dépend de "Département", et "Département" dépend de "EmployéID". Cela signifie que la relation entre "EmployéID" et "ResponsableDépartement" est transitive. Par exemple, l'employé 1 appartient au département "Informatique", dont le responsable est Alice.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_l.png)
