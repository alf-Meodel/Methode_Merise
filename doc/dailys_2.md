<a href="../README.md"><img src="../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_rt.png)

# Dailys 2 MERISE

![border](../assets/line/line-pink-point_l.png)

## Notes

```
CIF : regles de gestion bien goupillés
CIP: que les propriétés et attributs soient bien respectés
```

![border](../assets/line/border_deco_rb.png)

# Les cardinalités et les contraintes

![border](../assets/line/line-pink-point_r.png)

## Sommaire

- [x] [Les cardinalités](#les-cardinalités)

  - [x] Savoir lire les cardinalités :
  - [x] Savoir écrire les cardinalités :
  - [x] Savoir valider les cardinalités :

- [x] [Les différents types de contraintes](#les-differents-types-de-contraintes)
  - [x] Contraintes d'intégrité fonctionnelle
  - [x] [Savoir définir une contrainte d'intégrité] :
  - [x] Savoir différencier les types de contraintes :
  - [x] Contraintes d'intégrité physique :
- [x] [Les contraintes d'intégrité fonctionnelle (CIF)](#les-contraintes-dintégrité-fonctionnelle-cif)
  - [x] Savoir identifier une CIF :
  - [x] Savoir représenter une CIF sur le MCD :
  - [x] Savoir valider une CIF :
- [x] [Les contraintes d'intégrité physique](#contraintes-dintégrité-physique)
  - [x] Savoir identifier une contrainte physique :
  - [x] Savoir représenter une contrainte physique :
  - [x] Savoir valider une contrainte physique :

![border](../assets/line/line-pink-point_r.png)

## TABLEAU DES CONTRAINTES RECAP

| **Type**                     | **Explication imagée**                              | **Cas concret**                                                                   |
| ---------------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------- |
| Définir une contrainte       | "Un train doit avoir un conducteur."                | Un train doit être associé à un conducteur dans la base de données d'une gare.    |
| Différencier les contraintes | "Catégorie logique vs format technique."            | Fonctionnelle : Produit lié à Catégorie. Physique : Prix > 0.                     |
| Fonctionnelle                | "Une facture est liée à un client."                 | Une facture ne peut exister sans un client associé dans la base.                  |
| Physique                     | "Le mot de passe doit avoir au moins 8 caractères." | Le champ "Mot de passe" doit être non nul et respecter des contraintes de format. |

![border](../assets/line/border_deco_l.png)

# Les Cardinalités

![border](../assets/line/line-pink-point_r.png)

## Savoir lire les cardinalités

**Lire les cardinalités signifie comprendre les relations entre les entités dans un MCD :**

```
  Si je lis une cardinalité, je dois comprendre combien d'éléments d'une table sont liés à un ou plusieurs éléments d'une autre table.
```

### Explication imagée :

"Un client peut passer plusieurs commandes, mais un produit ne peut appartenir qu'à une seule catégorie." Lire les cardinalités, c'est comprendre le nombre minimum et maximum d'interactions entre les entités.

### Cas concret :

Prenons un magasin. La relation entre "Client" et "Commande" a une cardinalité (1,n) : un client passe au moins une commande (1) et peut en passer plusieurs (n). Du côté de "Commande", la cardinalité est (1,1) : une commande appartient à un client unique. Cela garantit qu'il n'y a pas de commande sans client.

### Exemples :

**(0,1) :** Une occurrence d'une entité peut être associée à zéro ou une occurrence d'une autre entité (relation optionnelle et unique).

**(1,n) :** Une occurrence d'une entité doit être associée à au moins une occurrence de l'autre entité, mais peut l’être plusieurs fois (relation obligatoire et multiple).

**(0,n) :** Une occurrence d'une entité peut être associée à zéro, une, ou plusieurs occurrences de l'autre entité (relation optionnelle et multiple).

**(1,1) :** Une occurrence d'une entité est associée obligatoirement à une seule occurrence de l'autre entité (relation obligatoire et unique).

![border](../assets/line/line-teal-point_r.png)

## Savoir écrire les cardinalités

```
Si j’écris une cardinalité, je dois indiquer combien d’éléments peuvent être liés entre deux tables (par exemple, un client peut avoir plusieurs commandes, mais une commande est pour un seul client).
```

### Explication imagée :

"Un livre est toujours dans une bibliothèque, mais une bibliothèque peut avoir plusieurs livres." Écrire les cardinalités, c'est traduire les règles métier en min/max pour chaque entité.

### Cas concret :

Dans une université, une relation "Cours-Étudiant" avec une cardinalité (1,n) pour "Étudiant" signifie qu'un étudiant suit au moins un cours et peut en suivre plusieurs. La cardinalité (1,30) pour "Cours" indique qu'un cours doit avoir au moins un étudiant inscrit, mais pas plus de 30.

---

### Pour écrire correctement les cardinalités dans un MCD, il faut :

#### Analyser les règles métier :

Les cardinalités doivent représenter fidèlement les exigences du domaine. Par exemple, si une règle métier stipule qu'un client doit avoir au moins un compte bancaire, cela signifie que la relation entre les entités "Client" et "Compte bancaire" aura une cardinalité (1,n) du côté de "Client" vers "Compte bancaire".

#### Utiliser les symboles appropriés :

Lors de la modélisation, écrivez les cardinalités à chaque extrémité des relations entre deux entités pour indiquer clairement la nature de la relation. Par exemple, si une commande peut être associée à plusieurs produits, vous pouvez écrire (1,n) du côté "Commande" vers "Produit".

![border](../assets/line/line-teal-point_r.png)

## Savoir valider les cardinalités

```
Si je valide une cardinalité, je dois m'assurer que les liens entre les éléments sont corrects et qu'ils reflètent bien les besoins du projet.
Les différents types de contraintes
```

### Explication imagée :

"Un employé doit appartenir à un service, mais un service peut exister sans employé." Valider les cardinalités, c'est vérifier qu'elles respectent les règles métier sans contradiction.

### Cas concret :

Dans une entreprise, la relation "Service-Employé" avec une cardinalité (1,n) pour "Employé" signifie qu'un employé doit obligatoirement être affecté à un service. Si un service est vide (0,n), cela respecte la règle métier. Tester la cardinalité garantit que les bases de données empêchent une incohérence.

---

### Définition :

La validation des cardinalités consiste à vérifier que les cardinalités définies respectent les règles métier et garantissent la logique et la cohérence du modèle.

### Vérifier les exigences du domaine :

Assurez-vous que chaque cardinalité respecte les contraintes de votre domaine métier. Par exemple, si une règle impose qu'un employé doit être affecté à au moins un département, une cardinalité (0,n) ne conviendrait pas ; il faudrait une cardinalité (1,n) pour respecter cette règle.

### Testez des scénarios :

En simulant des cas concrets, vous pouvez valider si les cardinalités permettent bien toutes les situations réelles possibles. Par exemple, si une relation est (1,1), vérifiez qu’il n'existe pas de cas d’utilisation où l’association devrait être optionnelle.

### Respecter la cohérence :

Les cardinalités doivent garantir l’intégrité du modèle ; elles ne doivent ni être trop restrictives ni trop permissives. Assurez-vous que les valeurs définies ne créent pas d'incohérences logiques dans le modèle.

En maîtrisant la lecture, l’écriture et la validation des cardinalités, on s’assure que le MCD est un reflet fidèle des contraintes et relations nécessaires pour le système d’information.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-pink-point_r.png)

# Les differents types de contraintes

![border](../assets/line/line-teal-point_r.png)

## Savoir définir une contrainte d'intégrité

```
Si je définis une contrainte d'intégrité, je dois m'assurer que les données sont correctes et cohérentes en suivant des règles précises.
```

### Explication imagée :

"Un train doit toujours avoir un conducteur pour partir." Une contrainte d'intégrité impose des règles qui assurent la cohérence des données entre deux entités ou au sein d'une entité.

### Cas concret :

Dans une base de données d'une gare, une contrainte impose qu'un "Train" doit avoir un conducteur attribué dans la table "Conducteurs". Si un train est ajouté sans conducteur, ou si le conducteur est supprimé sans mise à jour, cela viole la contrainte. Une contrainte d'intégrité évite cette incohérence.

![border](../assets/line/line-teal-point_r.png)

## Savoir différencier les types de contraintes

```
 Si je mets une ville, je dois m'assurer qu'elle existe dans la liste des villes autorisées.
```

### Définition :

Il existe deux types principaux de contraintes dans Merise : les contraintes d'intégrité fonctionnelle et les contraintes d'intégrité physique. Elles jouent un rôle complémentaire dans la gestion et la validation des données.

### Explication imagée :

"Un produit appartient à une catégorie (fonctionnelle) et son prix doit être positif (physique)." **Les contraintes fonctionnelles assurent la logique métier**, tandis que **les contraintes physiques imposent des règles sur le format et les valeurs des données**.

### Cas concret :

### Dans un système e-commerce :

- **Contrainte fonctionnelle :**

  "Un produit doit appartenir à une catégorie." Cela impose une relation logique entre "Produit" et "Catégorie".

- **Contrainte physique :**

  "Le prix du produit doit être un nombre positif." Cette contrainte vérifie que la valeur du champ "Prix" est correcte en termes de format et de contenu.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-pink-point_l.png)

# Les contraintes d'intégrité fonctionnelle (CIF)

![border](../assets/line/line-teal-point_r.png)

## Savoir identifier une CIF :

      Si j’identifie une CIF, je dois vérifier que chaque donnée dépend d'une autre de manière unique (par exemple, chaque numéro d'étudiant correspond à un seul étudiant).

### Explication imagée :

"Paris ne peut exister sans la France." Une CIF garantit qu'une donnée (ex. ville) est logique et dépend d'une autre (ex. pays) selon une règle métier.

### Cas concret :

Dans une base de données, si "Ville" est reliée à "Pays", une CIF stipule qu'une ville doit toujours être liée à un pays valide. Par exemple, si "Paris" est associée à "France", la suppression de "France" rendrait "Paris" incohérente. Une CIF empêche donc cette situation.

![border](../assets/line/line-teal-point_r.png)

## Savoir représenter une CIF sur le MCD :

      Si je représente une CIF sur le MCD, je dois l’indiquer par une relation qui assure l'unicité de la donnée (par exemple, un étudiant a un seul numéro de carte).

### Explication imagée :

"Chaque ville est rattachée à un pays dans le MCD." Représenter une CIF, c'est utiliser une relation avec des cardinalités pour illustrer cette dépendance logique.

### Cas concret :

Dans le MCD, la relation entre "Ville" et "Pays" est représentée par une entité "Ville" reliée à "Pays" avec une cardinalité (1,1) pour "Pays" et (0,n) pour "Ville". Cela signifie qu'un pays peut exister sans ville, mais une ville doit appartenir à un seul pays.

![border](../assets/line/line-teal-point_r.png)

## Savoir valider une CIF :

      Si je valide une CIF, je dois m'assurer que la contrainte est respectée dans la base de données et que chaque donnée est bien reliée de manière unique.

### Explication imagée :

"Supprimer la France doit empêcher de garder Paris." Valider une CIF, c'est tester qu'une règle métier logique est bien appliquée dans le système.

### Cas concret :

Pour valider la CIF "Une ville doit appartenir à un pays", testez dans la base qu'il est impossible d'insérer une ville sans pays existant. Par exemple, ajouter "Paris" sans "France" ou supprimer "France" tout en gardant "Paris" doit être interdit par la CIF.

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/line-pink-point_l.png)

# Contraintes d'intégrité physique

![border](../assets/line/line-teal-point_r.png)

## Savoir identifier une contrainte physique :

      Si j'identifie une contrainte physique, je dois m'assurer qu'elle est liée au stockage ou à l’organisation des données pour les protéger.(MLD ?)

### Explication imagée :

"Le code postal doit avoir 5 chiffres." Une contrainte physique impose des limites techniques ou de format à une donnée.

### Cas concret :

Dans une base de données, le champ "Code Postal" a une contrainte physique "INTEGER(5)" qui limite sa longueur à 5 chiffres. Cela empêche l'insertion de valeurs incorrectes, comme "123" ou "ABCDE", garantissant ainsi la validité des données.

![border](../assets/line/line-teal-point_r.png)

## Savoir représenter une contrainte physique :

      Si je représente une contrainte physique, je dois m'assurer qu'elle est appliquée dans le modèle physique de la base de données pour optimiser les performances ou la sécurité.

### Explication imagée :

"Chaque produit a un prix positif." Représenter une contrainte physique, c'est utiliser des types de données et des validations pour appliquer ces restrictions.

### Cas concret :

Dans le Modèle Physique de Données (MPD), un champ "Prix" est défini comme DECIMAL(10,2) NOT NULL CHECK (Prix > 0). Cela signifie que le prix doit être un nombre décimal, ne peut pas être vide, et doit être strictement positif. Ces règles sont directement implémentées dans la base.

![border](../assets/line/line-teal-point_r.png)

## Savoir valider une contrainte physique :

      Si je valide une contrainte physique, je dois m’assurer qu’elle fonctionne correctement et ne ralentit pas ou ne compromet pas l’intégrité des données.

### Explication imagée :

"Le système refuse un code postal à 4 chiffres." Valider une contrainte physique, c'est tester que les données incorrectes sont bien rejetées.

### Cas concret :

Pour valider la contrainte "Prix > 0", essayez d'insérer un produit avec un prix de -5 ou 0 dans la base. La base doit rejeter ces valeurs. De même, si un champ "Nom" est "NOT NULL", insérer un produit sans nom doit être interdit. Ces tests confirment que les contraintes physiques fonctionnent.

![border](../assets/line/line-pink-point_r.png)

<a href="#sommaire"><img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;"></a>

![border](../assets/line/border_deco_l.png)
