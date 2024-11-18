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

- [x] [Le graphe des dépendances](#le-graphe-des-dépendances)
  - [x] Savoir construire un graphe des dépendances
  - [x] Savoir valider un graphe des dépendances

![border](../assets/line/line-pink-point_l.png)

## Liens

- [Repo de Hachemi](https://github.com/HachemiH/formation-cda-bdd)

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

![border](../assets/line/line-teal-point_r.png)

# Les Formes Normales

![border](../assets/line/line-teal-point_r.png)

## Comprendre la 1ère forme normale (1FN)

### Explication imagée :

"Une boîte de rangement ne contient qu'un seul type d'éléments." La 1FN impose que chaque colonne ait des valeurs atomiques (non divisibles).

### Cas concret :

Une table contenant une colonne "Téléphones" avec des valeurs comme "06-12-34-56-78, 07-98-76-54-32" viole la 1FN. La 1FN exige une nouvelle ligne pour chaque numéro de téléphone, rendant les données plus exploitables et cohérentes.

## Table non normalisée (avant d’appliquer les formes normales) :

| **ID Commande** | **Client** | **Produit** | **Quantité** | **Prix Unitaire** | **Adresse Client**   |
| --------------- | ---------- | ----------- | ------------ | ----------------- | -------------------- |
| 1               | Alice      | T-shirt     | 2            | 10                | 10 rue des Lilas     |
| 1               | Alice      | Jean        | 1            | 30                | 10 rue des Lilas     |
| 2               | Bob        | Casquette   | 3            | 5                 | 20 avenue des Champs |
| 3               | Alice      | T-shirt     | 1            | 10                | 10 rue des Lilas     |

---

![border](../assets/line/line-teal-point_r.png)

## Comprendre la 1ère forme normale (1FN)

```
Si je valide la 1FN, je dois m'assurer que chaque colonne contient une valeur atomique (pas de liste ou tableau dans une cellule).

pas de nom prenom dans un meme champ
```

#### Une table est en 1ère forme normale (1FN) si elle respecte ces conditions :

- Pas de colonnes répétées : Chaque champ doit contenir une seule valeur (c’est-à-dire, pas de listes ou de groupes de valeurs dans une colonne).
- Toutes les valeurs doivent être atomiques : Chaque cellule doit contenir une seule valeur et non un groupe de valeurs.

## Problème avec la table actuelle :

La table ci-dessus respecte déjà la 1ère forme car chaque colonne contient des valeurs atomiques (pas de listes ou groupes dans les cellules). Les données sont bien organisées en colonnes simples.

---

![border](../assets/line/line-teal-point_r.png)

## Table en 1ère forme normale (1FN)

| **ID Commande** | **Client** | **Produit** | **Quantité** | **Prix Unitaire** | **Adresse Client**   |
| --------------- | ---------- | ----------- | ------------ | ----------------- | -------------------- |
| 1               | Alice      | T-shirt     | 2            | 10                | 10 rue des Lilas     |
| 1               | Alice      | Jean        | 1            | 30                | 10 rue des Lilas     |
| 2               | Bob        | Casquette   | 3            | 5                 | 20 avenue des Champs |
| 3               | Alice      | T-shirt     | 1            | 10                | 10 rue des Lilas     |

---

À ce stade, nous sommes en 1FN : chaque cellule contient une seule valeur, et chaque ligne est une combinaison unique d’informations.

![border](../assets/line/line-pink-point_r.png)

## Comprendre la 2ème forme normale (2FN)

```
Si je valide la 2FN, je dois m'assurer qu'il n'y a aucune dépendance partielle entre les attributs d'une table et sa clé primaire.

a: dans la table etudiant on ne doit pas retrouver des informations sur la classe , non de la classe etc
```

![border](../assets/line/border-teal-t.png)

## Tips de cours

```

def type : un attribut non identifiant ne dépend pas d'une partie de l'identifiant mais de tout l'identifiant

((Numéro de commande | Numéro du produit)) | (Date de commande)
on suppose que id concerne les deux premeirs
mais numéro de commande est affilié à Date de commande
alros on le sort pour leplacer avec date commande

```

![border](../assets/line/border-teal-b.png)

### Explication imagée :

"Un cahier d'élèves n'a qu'une seule liste par page." La 2FN supprime les dépendances partielles entre une colonne non clé et une partie d’une clé primaire.

### Cas concret :

Une table "Commandes" avec une clé primaire composée de "CommandeID" et "ProduitID", où "PrixProduit" dépend uniquement de "ProduitID", viole la 2FN. La 2FN exige de séparer les produits dans une table à part, liée par "ProduitID".

---

### Définition :

Une table est en 2ème forme normale (2FN) si elle est déjà en 1ère forme normale (1FN) et que toutes les colonnes non-clés dépendent entièrement de la clé primaire. En d’autres termes, il ne doit pas y avoir de dépendances partielles.

## Problèmes dans la table actuelle :

- L’adresse client dépend du client (pas de la commande). Cela signifie qu'il y a une dépendance partielle :
- l’adresse du client n’a pas besoin de répéter à chaque ligne de commande, elle peut être enregistrée une seule fois pour ce client.

## Solution pour passer à la 2FN :

Séparer les informations sur les clients dans une table distincte.
Créer une table de commandes qui ne contient que les informations liées à chaque commande spécifique.
Une table produits contenant les détails du produit acheté.

## Table Clients (après 2ème forme normale - 2FN)

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

### Avantages de la 2FN :

### Suppression de la redondance :

L’adresse du client est maintenant séparée dans une table Clients. Si Alice déménage, on n’a plus besoin de mettre à jour chaque ligne de commande, juste la ligne correspondante dans la table des Clients.
La table est maintenant plus efficace et plus facile à maintenir.

---

![border](../assets/line/line-teal-point_r.png)

## Comprendre la 3ème forme normale (3FN)

```
Si je valide la 3FN, je dois m'assurer qu'il n'y a aucune dépendance transitive entre les attributs d'une table et sa clé primaire.

```

### Explication imagée :

"Un arbre de famille sans branches inutiles." La 3FN élimine les dépendances transitives, où une colonne dépend d'une autre colonne non clé via une colonne intermédiaire.

### Cas concret :

Dans une table "Employés" avec "EmployéID", "Département", et "ResponsableDépartement", si "ResponsableDépartement" dépend de "Département", cela viole la 3FN. La 3FN impose de créer une table séparée "Départements".

---

### Définition :

Une table est en 3ème forme normale (3FN) si elle est déjà en 2ème forme normale (2FN) et qu’il n’y a pas de dépendances transitives entre les colonnes non-clés.

Une dépendance transitive se produit quand une colonne non-clé dépend d’une autre colonne non-clé via une clé primaire.

---

### Problèmes dans la table actuelle (en 2FN) :

Dans la table Commandes, nous avons une dépendance transitive :

Prix Unitaire dépend de Produit, mais Produit dépend de ID Commande (via la table des produits). Donc, Prix Unitaire est transitivement dépendant de ID Commande via Produit.

### Solution pour passer à la 3FN :

Séparer l’information sur les produits dans une table distincte.
Prix Unitaire ne doit pas être dans la table Commandes. Il doit être enregistré dans une table Produits indépendante.

## Table Commandes (après 3ème forme normale - 3FN)

| **ID Commande** | **ID Client** | **ID Produit** | **Quantité** |
| --------------- | ------------- | -------------- | ------------ |
| 1               | 1             | 1              | 2            |
| 1               | 1             | 2              | 1            |
| 2               | 2             | 3              | 3            |
| 3               | 1             | 1              | 1            |

---

## Table Produits (après 3ème forme normale - 3FN)

| **ID Produit** | **Produit** | **Prix Unitaire** |
| -------------- | ----------- | ----------------- |
| 1              | T-shirt     | 10                |
| 2              | Jean        | 30                |
| 3              | Casquette   | 5                 |

---

---

## Table Clients (inchangée après 3ème forme normale - 3FN)

| **ID Client** | **Client** | **Adresse Client**   |
| ------------- | ---------- | -------------------- |
| 1             | Alice      | 10 rue des Lilas     |
| 2             | Bob        | 20 avenue des Champs |

### Avantages de la 3FN :

### Suppression des dépendances transitives :

Les informations sur le prix sont séparées de la table Commandes et sont gérées dans la table Produits.
Chaque table contient uniquement des informations qui dépendent directement de la clé primaire, ce qui permet de mieux organiser la base et de faciliter sa gestion.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-teal-point_r.png)

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

## Le Graphe des dépendances

### Savoir construire un graphe des dépendances :

```
Si je construis un graphe des dépendances, je dois représenter visuellement les relations entre les attributs pour en faciliter l’analyse.
```

### Explication imagée :

"Un schéma d'organisation d'entreprise." Construire un graphe des dépendances, c’est représenter visuellement comment les colonnes d’une table dépendent les unes des autres.

### Cas concret :

| **ProduitID** | **Catégorie** | **ResponsableCatégorie** |
| ------------- | ------------- | ------------------------ |
| 1             | Vêtements     | Alice                    |
| 2             | Électronique  | Bob                      |
| 3             | Vêtements     | Alice                    |

Dans cette table "Produits", "Catégorie" dépend de "ProduitID", et "ResponsableCatégorie" dépend de "Catégorie". Par exemple, le produit 1 appartient à la catégorie "Vêtements", dont le responsable est Alice. Cette dépendance est facilement visualisable dans un graphe.

## Savoir valider un graphe des dépendances :

```
Si je valide un graphe des dépendances, je dois m'assurer qu'il reflète correctement toutes les relations de dépendance fonctionnelle de la table.
```

### Explication imagée :

"Vérifiez que toutes les flèches mènent au bon endroit." Valider un graphe des dépendances, c’est s’assurer qu’il reflète toutes les relations logiques correctes.

### Cas concret :

| **FactureID** | **Client** | **AdresseClient**    |
| ------------- | ---------- | -------------------- |
| 1             | Alice      | 10 rue des Lilas     |
| 2             | Bob        | 20 avenue des Champs |
| 3             | Carol      | 30 avenue de la Lune |

Dans cette table "Factures", "AdresseClient" dépend de "Client", qui dépend de "FactureID". Cela signifie qu’on ne peut accéder à l’adresse du client que via le client associé à une facture donnée. Par exemple, la facture 1 est liée à Alice, dont l’adresse est "10 rue des Lilas". Si une flèche est incorrecte ou manquante dans le graphe, la validation échoue.

---

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_l.png)
