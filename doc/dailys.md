 <a href="../README.md">
  <img src="../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_rt.png)

# Dailys

![border](../assets/line/line-pink-point_l.png)

## Sommaire

- [Cardinalités](#les-cardinalités)
- [Lire les Cardinalités](#savoir-lire-les-cardinalités)

![border](../assets/line/border_deco_rb.png)

# Objectifs journaliers

![border](../assets/line/line-pink-point_r.png)

##### Jeudi 14/11/2024 :

### MERISE - Les cardinalités et les contraintes

- [x] Les cardinalités

  - [x] Savoir lire les cardinalités
  - [x] Savoir écrire les cardinalités
  - [x] Savoir valider les cardinalités

- [ ] Les différents types de contraintes

  - [ ] Savoir définir une contrainte d'intégrité
  - [ ] Savoir différencier les types de contraintes :
    - [ ] Contraintes d'intégrité fonctionnelle
    - [ ] Contraintes d'intégrité physique

- [ ] Les contraintes d'intégrité fonctionnelle (CIF)

  - [ ] Savoir identifier une CIF
  - [ ] Savoir représenter une CIF sur le MCD
  - [ ] Savoir valider une CIF

- [ ] Les contraintes d'intégrité physique
  - [ ] Savoir identifier une contrainte physique
  - [ ] Savoir représenter une contrainte physique
  - [ ] Savoir valider une contrainte physique

![border](../assets/line/line-teal-point_l.png)

# Les Cardinalités

![border](../assets/line/line-pink-point_r.png)

## Savoir lire les cardinalités

**Lire les cardinalités signifie comprendre les relations entre les entités dans un MCD, notamment :**

### Interpréter les symboles :

Les cardinalités sont souvent indiquées entre parenthèses, comme (0,1), (1,1), (0,n), (1,n). Le premier chiffre représente la cardinalité minimale (le nombre minimum de fois où une instance d'une entité peut être associée à une autre entité), et le deuxième chiffre représente la cardinalité maximale (le nombre maximum de fois où une instance d'une entité peut être associée à l'autre entité).

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
<a href="#sommaire">
<img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_l.png)
