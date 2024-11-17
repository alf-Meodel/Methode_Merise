 <a href="../README.md">
  <img src="../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_rt.png)

# Dailys 3 MERISE

![border](../assets/line/line-pink-point_l.png)

## Notes

```
CIF : regles de gestion bien goupillés
CIP: que les propriétés et attributs soient bien respectés
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

![border](../assets/line/line-teal-point_r.png)

# Introduction à la normalisation

## Comprendre l'importance de la normalisation

```
Si je comprends l'importance de la normalisation, je peux identifier et réduire les anomalies dans une base de données pour améliorer sa cohérence.
```

## Savoir identifier les anomalies de redondance

```
Si je repère une redondance, je dois m'assurer qu'elle peut être éliminée en décomposant les données sans perdre d'information
```

## Définition

- La normalisation est le processus qui permet d’organiser les données dans une base pour éviter la duplication, améliorer l’efficacité et garantir la cohérence des informations.

- Elle permet de réduire les risques d’erreurs et de faciliter les mises à jour et la maintenance des données.

## Rien ne vaut un bon exemple

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

#### Réduction de la redondance :

L’adresse de Alice n’apparaît qu’une seule fois dans la table Clients.
Le titre du livre "Harry Potter" apparaît uniquement dans la table Livres, et non plus plusieurs fois dans la table des emprunts.
#### Facilité de mise à jour :

Si Alice change d’adresse, il suffit de la mettre à jour dans une seule ligne de la table Clients. Pas besoin de modifier plusieurs lignes dans la table des emprunts.

#### Gestion plus simple :

Les informations sont organisées. Si tu veux savoir quels livres Alice a empruntés, tu peux consulter la table Emprunts en liant l’ID Client à la table Clients et l’ID Livre à la table Livres. C’est beaucoup plus simple à gérer et à mettre à jour.

#### Conclusion Définition
La normalisation permet d’organiser les données de manière plus logique et efficace. Grâce à cela, tu évites de répéter des informations, tu réduis les erreurs possibles et tu facilites les mises à jour. C’est un peu comme ranger tes jouets dans des boîtes distinctes pour ne pas avoir un bazar dans ta chambre !

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-teal-point_r.png)

# Les Formes Normales

![border](../assets/line/line-teal-point_r.png)

## Cas concret

### Base de données des commandes dans un magasin

Imaginons qu’on gère une base de données pour un magasin qui enregistre les commandes de ses clients. La table suivante contient des informations sur les commandes passées par les clients, les produits achetés et les quantités.

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

![border](../assets/line/line-teal-point_r.png)

## Comprendre la 2ème forme normale (2FN)

```
Si je valide la 2FN, je dois m'assurer qu'il n'y a aucune dépendance partielle entre les attributs d'une table et sa clé primaire.
```

#### Définition de la 2ème forme normale (2FN) :

Une table est en 2ème forme normale (2FN) si elle est déjà en 1ère forme normale (1FN) et que toutes les colonnes non-clés dépendent entièrement de la clé primaire. En d’autres termes, il ne doit pas y avoir de dépendances partielles.

### Clé primaire :

une clé qui permet d'identifier de manière unique chaque ligne de la table. Ici, ID Commande peut être une clé primaire, mais il y a une dépendance partielle (par exemple, l’adresse du client dépend du Client, et non de la commande).

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

##### Suppression de la redondance :

L’adresse du client est maintenant séparée dans une table Clients. Si Alice déménage, on n’a plus besoin de mettre à jour chaque ligne de commande, juste la ligne correspondante dans la table des Clients.
La table est maintenant plus efficace et plus facile à maintenir.

---

![border](../assets/line/line-teal-point_r.png)

## Comprendre la 3ème forme normale (3FN)

```
Si je valide la 3FN, je dois m'assurer qu'il n'y a aucune dépendance transitive entre les attributs d'une table et sa clé primaire.
```

### Définition de la 3ème forme normale (3FN) :

Une table est en 3ème forme normale (3FN) si elle est déjà en 2ème forme normale (2FN) et qu’il n’y a pas de dépendances transitives entre les colonnes non-clés.

Une dépendance transitive se produit quand une colonne non-clé dépend d’une autre colonne non-clé via une clé primaire.

### Problèmes dans la table actuelle (en 2FN) :

Dans la table Commandes, nous avons une dépendance transitive :

Prix Unitaire dépend de Produit, mais Produit dépend de ID Commande (via la table des produits). Donc, Prix Unitaire est transitivement dépendant de ID Commande via Produit.

## Solution pour passer à la 3FN :

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

### Conclusion :

#### 1ère forme normale (1FN) :

Assure que chaque valeur dans une cellule est atomique.

#### 2ème forme normale (2FN) :

Élimine les dépendances partielles (chaque colonne non-clé dépend complètement de la clé primaire).

#### 3ème forme normale (3FN) :

Élimine les dépendances transitives entre les colonnes non-clés.
Ces étapes de normalisation permettent de rendre la base de données plus efficace, cohérente, et plus facile à maintenir.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-teal-point_r.png)

# Dépendances Fonctionnelles

## Savoir identifier les DF élémentaires

```
Si j'identifie une dépendance fonctionnelle élémentaire, je dois m'assurer qu'un attribut dépend uniquement d'une autre colonne.
```

Une dépendance fonctionnelle élémentaire (DF élémentaire) implique un seul attribut (ou ensemble minimal d'attributs) qui détermine un autre attribut.

### Exemple concret :

Imaginons une table Étudiants avec les colonnes :

ID Étudiant
Nom
Prénom
Matière
On peut avoir la dépendance suivante :

Copier le code
ID Étudiant → Nom
Cela signifie que l'ID Étudiant détermine de manière unique le Nom de l'étudiant.

Ici, la DF élémentaire est une relation simple entre un seul attribut (ID Étudiant) et un autre attribut (Nom).

Autre exemple :
Copier le code
Matière → Professeur
Cela signifie qu'une matière détermine un seul professeur.

## Savoir identifier les DF composées

```
Si j'identifie une dépendance fonctionnelle composée, je dois vérifier qu'elle implique plusieurs attributs pour déterminer une valeur.
```

Une dépendance fonctionnelle composée est une dépendance fonctionnelle dans laquelle un ensemble d'attributs détermine un autre attribut. Il ne s'agit pas d'une dépendance entre un seul attribut, mais d'un groupe d'attributs.

Exemple concret :
Imaginons une table Ventes avec les colonnes :

ID Vente
ID Produit
Quantité
Prix Unitaire
Montant
On peut avoir la dépendance suivante :

scss
Copier le code
(ID Vente, ID Produit) → Montant
Cela signifie que l'ensemble d'attributs (ID Vente et ID Produit) détermine de manière unique le Montant de la vente.

Ici, il ne s'agit pas d'une seule colonne déterminant une autre, mais bien de deux attributs combinés qui déterminent une autre colonne.

## Savoir identifier les DF transitives

```
Si j'identifie une dépendance fonctionnelle transitive, je dois m'assurer qu'un attribut dépend indirectement de la clé primaire via un autre attribut.
```

Une dépendance fonctionnelle transitive se produit lorsqu'un attribut dépend d'un autre attribut via un troisième attribut. En d'autres termes, une colonne A détermine B, et B détermine C. Par conséquent, on peut dire que A détermine C, mais ce lien est indirect.

Exemple concret :
Imaginons une table Commandes avec les colonnes :

ID Commande
ID Client
Nom Client
Adresse Client
On a les dépendances suivantes :

ID Commande → ID Client (chaque commande est associée à un client unique)
ID Client → Nom Client (un client est identifié par son nom)
ID Client → Adresse Client (un client est associé à une adresse)
La dépendance transitive est donc :

arduino
Copier le code
ID Commande → Nom Client
Bien que l'ID Commande détermine directement l'ID Client, et que ID Client détermine Nom Client, il y a une dépendance indirecte de ID Commande → Nom Client par le biais de ID Client.

Autre exemple de dépendance transitive :
Copier le code
Matricule → Nom
Nom → Salaire
Cela signifie que Matricule → Nom, et que Nom → Salaire. Par transitivité, Matricule → Salaire, bien que Matricule ne détermine pas directement Salaire.

Résumé des types de dépendances fonctionnelles
DF élémentaire : Une seule colonne détermine une autre colonne.

Exemple : ID Étudiant → Nom
DF composée : Un ensemble d'attributs détermine une autre colonne.

Exemple : (ID Vente, ID Produit) → Montant
DF transitive : Une dépendance indirecte entre deux attributs via un troisième attribut.

Exemple : ID Commande → Nom Client (via ID Client)
Conclusion :
Comprendre les dépendances fonctionnelles est essentiel pour bien structurer une base de données. Cela permet de mieux organiser les données, de prévenir les anomalies, et de garantir l'intégrité de la base en respectant les formes normales.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

## Le Graphe des dépendances

## Savoir construire un graphe des dépendances :

```
Si je construis un graphe des dépendances, je dois représenter visuellement les relations entre les attributs pour en faciliter l’analyse.
```

## Savoir valider un graphe des dépendances :

```
Si je valide un graphe des dépendances, je dois m'assurer qu'il reflète correctement toutes les relations de dépendance fonctionnelle de la table.
```

---

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_l.png)
