 <a href="../README.md">
  <img src="../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_rt.png)

# Dailys 2

![border](../assets/line/line-pink-point_l.png)

## Sommaire

- [Cardinalités](#les-cardinalités)
  - [Lire les Cardinalités](#savoir-lire-les-cardinalités)
  - []()

## Notes

CIF : regles de gestion bien goupillés

CIP: que les propriétés et attributs soient bien respectés

![border](../assets/line/border_deco_rb.png)

# Objectifs journaliers

![border](../assets/line/line-pink-point_r.png)

##### Jeudi 14/11/2024 :

### MERISE - Les cardinalités et les contraintes

- [x] Les cardinalités
- [x] Savoir lire les cardinalités :

  _Si je lis une cardinalité, je dois comprendre combien d'éléments d'une table sont liés à un ou plusieurs éléments d'une autre table._

- [x] Savoir écrire les cardinalités :
      Si j’écris une cardinalité, je dois indiquer combien d’éléments peuvent être liés entre deux tables (par exemple, un client peut avoir plusieurs commandes, mais une commande est pour un seul client).

- [x] Savoir valider les cardinalités :
      Si je valide une cardinalité, je dois m'assurer que les liens entre les éléments sont corrects et qu'ils reflètent bien les besoins du projet.
      Les différents types de contraintes

- [x] Savoir définir une contrainte d'intégrité :
      Si je définis une contrainte d'intégrité, je dois m'assurer que les données sont correctes et cohérentes en suivant des règles précises.

- [x] Savoir différencier les types de contraintes :

## Contraintes d'intégrité fonctionnelle :

Si je mets une ville, je dois m'assurer qu'elle existe dans la liste des villes autorisées.

- [x] Contraintes d'intégrité physique :
      Si j’utilise une contrainte physique, je dois m’assurer qu’elle est appliquée au niveau du modèle logique de données (MLD).
- [x] Les contraintes d'intégrité fonctionnelle (CIF)
- [x] Savoir identifier une CIF :
      Si j’identifie une CIF, je dois vérifier que chaque donnée dépend d'une autre de manière unique (par exemple, chaque numéro d'étudiant correspond à un seul étudiant).

- [x] Savoir représenter une CIF sur le MCD :
      Si je représente une CIF sur le MCD, je dois l’indiquer par une relation qui assure l'unicité de la donnée (par exemple, un étudiant a un seul numéro de carte).

- [x] Savoir valider une CIF :
      Si je valide une CIF, je dois m'assurer que la contrainte est respectée dans la base de données et que chaque donnée est bien reliée de manière unique.

- [x] Les contraintes d'intégrité physique
- [x] Savoir identifier une contrainte physique :
      Si j'identifie une contrainte physique, je dois m'assurer qu'elle est liée au stockage ou à l’organisation des données pour les protéger.

- [x] Savoir représenter une contrainte physique :
      Si je représente une contrainte physique, je dois m'assurer qu'elle est appliquée dans le modèle physique de la base de données pour optimiser les performances ou la sécurité.

- [x] Savoir valider une contrainte physique :

Si je valide une contrainte physique, je dois m’assurer qu’elle fonctionne correctement et ne ralentit pas ou ne compromet pas l’intégrité des données.

![border](../assets/line/line-teal-point_l.png)

# Les Cardinalités

![border](../assets/line/line-pink-point_r.png)

## Savoir lire les cardinalités

**Lire les cardinalités signifie comprendre les relations entre les entités dans un MCD, notamment :**

![border](../assets/line/line-teal-point_r.png)

### Interpréter les symboles :

Les cardinalités sont souvent indiquées entre parenthèses, comme (0,1), (1,1), (0,n), (1,n). Le premier chiffre représente la cardinalité minimale (le nombre minimum de fois où une instance d'une entité peut être associée à une autre entité), et le deuxième chiffre représente la cardinalité maximale (le nombre maximum de fois où une instance d'une entité peut être associée à l'autre entité).

![border](../assets/line/line-teal-point_r.png)

### Exemples :

**(0,1) :** Une occurrence d'une entité peut être associée à zéro ou une occurrence d'une autre entité (relation optionnelle et unique).
**(1,n) :** Une occurrence d'une entité doit être associée à au moins une occurrence de l'autre entité, mais peut l’être plusieurs fois (relation obligatoire et multiple).
**(0,n) :** Une occurrence d'une entité peut être associée à zéro, une, ou plusieurs occurrences de l'autre entité (relation optionnelle et multiple).
**(1,1) :** Une occurrence d'une entité est associée obligatoirement à une seule occurrence de l'autre entité (relation obligatoire et unique).

## Savoir écrire les cardinalités

Pour écrire correctement les cardinalités dans un MCD, il faut :

#### Analyser les règles métier :

Les cardinalités doivent représenter fidèlement les exigences du domaine. Par exemple, si une règle métier stipule qu'un client doit avoir au moins un compte bancaire, cela signifie que la relation entre les entités "Client" et "Compte bancaire" aura une cardinalité (1,n) du côté de "Client" vers "Compte bancaire".

#### Utiliser les symboles appropriés :

Lors de la modélisation, écrivez les cardinalités à chaque extrémité des relations entre deux entités pour indiquer clairement la nature de la relation. Par exemple, si une commande peut être associée à plusieurs produits, vous pouvez écrire (1,n) du côté "Commande" vers "Produit".

![border](../assets/line/line-teal-point_r.png)

## Savoir valider les cardinalités

La validation des cardinalités consiste à vérifier que les cardinalités définies respectent les règles métier et garantissent la logique et la cohérence du modèle.

#### Vérifier les exigences du domaine :

Assurez-vous que chaque cardinalité respecte les contraintes de votre domaine métier. Par exemple, si une règle impose qu'un employé doit être affecté à au moins un département, une cardinalité (0,n) ne conviendrait pas ; il faudrait une cardinalité (1,n) pour respecter cette règle.

#### Testez des scénarios :

En simulant des cas concrets, vous pouvez valider si les cardinalités permettent bien toutes les situations réelles possibles. Par exemple, si une relation est (1,1), vérifiez qu’il n'existe pas de cas d’utilisation où l’association devrait être optionnelle.

#### Respecter la cohérence :

Les cardinalités doivent garantir l’intégrité du modèle ; elles ne doivent ni être trop restrictives ni trop permissives. Assurez-vous que les valeurs définies ne créent pas d'incohérences logiques dans le modèle.

En maîtrisant la lecture, l’écriture et la validation des cardinalités, on s’assure que le MCD est un reflet fidèle des contraintes et relations nécessaires pour le système d’information.

![border](../assets/line/line-teal-point_r.png)

## Savoir définir une contrainte d'intégrité

![border](../assets/line/line-teal-point_r.png)

Une contrainte d'intégrité est une règle qui garantit que les données dans la base de données respectent certaines conditions pour qu'elles soient valides et cohérentes. Ces contraintes permettent de s'assurer que les informations stockées sont logiques, sans erreurs et respectent des règles précises.

### Les types de contraintes d'intégrité

Il y a plusieurs types de contraintes d'intégrité :

#### Contrainte d'intégrité de domaine :

Elle vérifie que les valeurs des attributs respectent un certain type ou format (par exemple, une date de naissance ne peut pas être dans le futur).

#### Contrainte d'intégrité de clé :

Elle vérifie que certaines valeurs (comme les clés primaires) sont uniques et non nulles.

#### Contrainte d'intégrité référentielle :

Elle garantit que les relations entre les tables sont respectées (par exemple, une classe doit exister avant d'assigner un élève à cette classe).

#### Contrainte d'intégrité fonctionnelle (celle dont nous parlons ici) :

Elle définit une règle sur la relation entre les attributs dans une table, en indiquant qu'une information (ou un ensemble d'informations) détermine de manière unique une autre information.

![border](../assets/line/line-teal-point_r.png)

## Savoir différencier les types de contraintes

![border](../assets/line/line-teal-point_r.png)

Il existe deux types principaux de contraintes dans Merise : les contraintes d'intégrité fonctionnelle et les contraintes d'intégrité physique. Elles jouent un rôle complémentaire dans la gestion et la validation des données.

#### Cas concret :

Imaginons une bibliothèque où chaque livre a un code unique (comme un code-barres). Si on doit retrouver un livre spécifique, le code unique permet d’être sûr qu’on a le bon livre sans risque de confusion avec un autre. Dans une base de données, ce type de contrainte s’assure que chaque élément important est unique, comme un numéro de carte pour chaque élève.

![border](../assets/line/line-teal-point_r.png)

## Contraintes d'intégrité fonctionnelle

![border](../assets/line/line-teal-point_r.png)

### Définition :

Les contraintes d'intégrité fonctionnelle (CIF) définissent les règles métiers ou les relations logiques que doivent respecter les données pour rester cohérentes avec le modèle conceptuel. Ces contraintes sont souvent liées à des règles métier spécifiques et sont définies dans le modèle conceptuel de données (MCD). Elles incluent :

- Unicité : assure qu’une donnée est unique dans la base, comme un numéro de sécurité sociale.
- Validation de valeurs : impose des limites ou des valeurs spécifiques, comme une contrainte pour des dates de naissance ou des codes postaux.
- Relations obligatoires : garantit qu'une entité doit être associée à une autre. Par exemple, un employé doit être affecté à un département.

  Ces contraintes sont plus abstraites et reflètent les spécificités du domaine métier. Elles n’ont pas de lien direct avec la structure physique de la base de données mais influencent sa logique.

  ### Vulgarisation

  Imagine que tu as un coffre où tu ranges tous tes jouets. Tu décides de créer une règle pour t’aider à tout garder en ordre. Cette règle dit :
  "Chaque jouet doit avoir sa propre place unique dans le coffre."

Alors, tu sais que ton ours en peluche doit toujours être dans le coin droit, tes voitures doivent être dans la boîte rouge, et ta poupée doit être sur l'étagère du milieu. Cette règle, c'est comme une contrainte d'intégrité fonctionnelle ! Elle aide à s'assurer que chaque jouet a un endroit spécial et qu’on ne se trompe pas en les rangeant.

### Cas concret :

Dans une bibliothèque, chaque livre a un numéro unique pour qu’on sache exactement où le trouver. C’est pareil dans une base de données : chaque donnée doit être unique pour qu’on puisse la retrouver facilement.

![border](../assets/line/line-teal-point_r.png)

## Contraintes d'intégrité physique

![border](../assets/line/line-teal-point_r.png)

### Definition

Les contraintes d'intégrité physique sont des règles qui assurent l'intégrité des données au niveau de la base physique, en garantissant la structure et la relation entre les tables. Elles sont définies au niveau du modèle logique de données (MLD) et sont mises en œuvre dans le modèle physique de données (MPD). Elles incluent :

- Clé primaire : une contrainte d'unicité et d'identification pour chaque ligne d’une table.
- Clé étrangère : assure la relation entre deux tables et garantit que les valeurs d'une table sont conformes aux valeurs de référence d'une autre table (par exemple, un département existant auquel un emsployé est affecté).

- Non nullité : impose que certains attributs (champs) doivent contenir une valeur non nulle, assurant que certaines informations sont toujours présentes dans la base.
  Les contraintes d'intégrité physique sont appliquées pour maintenir les données correctement reliées et éviter les incohérences, comme la suppression d’un enregistrement référencé.

### Vulgarisation :

Maintenant, imagine une autre règle pour ton coffre de jouets. Elle dit :
"Les jouets lourds vont en bas, et les jouets légers vont en haut."

Si tu mets les jouets lourds au-dessus, ils risquent d’écraser les plus légers, ou de tout faire tomber ! Alors, cette règle sert à ranger tes jouets en pensant à leur poids, pour que rien ne se casse. C’est une contrainte d’intégrité physique ! Elle aide à protéger tes jouets en respectant leur poids et leur taille.

![border](../assets/line/line-teal-point_r.png)
<a href="#sommaire">
<img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_l.png)
