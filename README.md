# Guide d'Introduction à Redis via CLI  
Ce projet propose un guide pratique et détaillé pour découvrir Redis, une base de données NoSQL clé/valeur rapide et performante. Vous apprendrez à installer Redis, à manipuler des données via la CLI, et à explorer ses principales fonctionnalités.  
## Table des Matières  
- [Introduction](#introduction)  
- [Bases de Données SQL et NoSQL](#bases-de-données-sql-et-nosql)  
  - [Approche SQL](#approche-sql)  
  - [Approche NoSQL](#approche-nosql)  
  - [Avantages et Inconvénients](#avantages-et-inconvénients)  
- [Les 4 Familles des Bases de Données NoSQL](#les-4-familles-des-bases-de-données-nosql)  
- [Introduction à Redis](#introduction-à-redis)  
  - [Prérequis](#prérequis)  
  - [Installation avec Docker](#installation-avec-docker)  
- [Tester Redis](#tester-redis)  
- [Premiers Pas avec Redis CLI](#premiers-pas-avec-redis-cli)  
  - [Définir une Clé/Valeur](#définir-une-clévaleur)  
  - [Incrémenter un Compteur](#incrémenter-un-compteur)  
  - [Expiration d’une Clé](#expiration-dune-clé)  
- [Travailler avec d’autres Structures de Données](#travailler-avec-dautres-structures-de-données)  
  - [Les Listes](#les-listes)  
  - [Les Ensembles](#les-ensembles)  
  - [Ensembles Ordonnés (Sorted Set)](#ensembles-ordonnés-sorted-set)  
  - [Hashmaps (Hash)](#hashmaps-hash)
  - [HyperLogLog](#hyperloglog)
- [Persistance et Limites de Redis](#persistance-et-limites-de-redis)  
## Introduction  
Les bases de données sont essentielles pour gérer les informations dans les applications modernes, comme les sites e-commerce ou les applications mobiles. Traditionnellement, les bases de données relationnelles (SQL) étaient les plus courantes, grâce à leur structure et leur fiabilité.  

Cependant, avec l'augmentation des volumes de données et les besoins en performance, les bases de données NoSQL ont gagné en popularité.  

Ce rapport 📝 va :  
- Comparer les bases de données SQL et NoSQL.  
- Explorer les principales familles de NoSQL : clé/valeur, colonne, document, et graphe.  
- Se concentrer sur les bases de données clé/valeur, en particulier Redis.  

L'objectif est d’offrir une introduction claire et accessible, même sans expérience préalable en bases de données.  
## Bases de Données SQL et NoSQL  

### Approche SQL  

Imaginez que vous organisez une fête d'anniversaire pour vos amis. Vous décidez de noter leurs préférences culinaires dans un tableau structuré :  

| Nom   | Allergies   | Plat préféré   |  
|-------|-------------|----------------|  
| Marie | Lactose     | Curry          |  
| Jean  | Gluten      | Pizza          |  

C’est parfait pour éviter les erreurs, mais cela pose problème si un ami arrive avec une demande spécifique, comme :  
*« Je veux des nuggets, mais uniquement ceux en forme de dinosaure. »*  

Pour gérer ce type de demande, vous devrez soit modifier toute la structure du tableau, soit tout réorganiser.  

🌟 **Ce qu’il faut retenir** :  
- Parfait pour des données organisées et des relations complexes.  
- Peu adapté aux changements fréquents ou imprévus.  

---

### Approche NoSQL  

Dans cette approche, vous utilisez des post-its pour noter les préférences :  
- Jean : "Pas de gluten, adore les pizzas."  
- Marie : "Végétarienne, aime le curry."  
- Luc : "Pas fan des champignons."  

Cela permet une grande flexibilité, mais peut compliquer la recherche de données précises.  

![image](https://github.com/user-attachments/assets/1197448e-e414-4e46-9d7c-d0f24f097afc)

🌟 **Ce qu’il faut retenir** :  
- Flexible et adapté à des données variées.  
- Moins efficace pour interroger des relations complexes.  

---

### Avantages et Inconvénients  

![image](https://github.com/user-attachments/assets/2e8e089b-9ecd-4fca-bbb1-2c167db82a00)


---

## Les 4 Familles des Bases de Données NoSQL  

1. **Clé/Valeur (Key/Value)**  
   Comme un dictionnaire, chaque clé pointe vers une valeur unique.  

![image](https://github.com/user-attachments/assets/344bd079-0a9d-4731-8b53-737e76038068)

![image](https://github.com/user-attachments/assets/3d0be589-00ac-4742-9f23-2af8b66ae2b1)


2. **Colonnes (Column-Family Stores)**  
   Données organisées par colonnes, adaptées aux grandes quantités de données.  

![image](https://github.com/user-attachments/assets/c747d2e1-1715-482f-907e-266bf48b0609)


3. **Documents (Document-Oriented Databases)**  
   Données stockées sous forme de documents JSON ou XML.  

![image](https://github.com/user-attachments/assets/a7bb5d92-1f4e-4242-95c3-bcd52bf36374)

4. **Graphes (Graph)**  
   Parfait pour représenter des relations complexes entre entités (ex. réseaux sociaux).  

![image](https://github.com/user-attachments/assets/5682b1d1-c323-479f-95e6-fad855069f85)

## Introduction à Redis  
Redis (Remote Dictionary Server) est une base de données NoSQL clé/valeur rapide et légère, conçue pour fonctionner principalement en mémoire.  

### Prérequis  
- Installer [Docker](https://www.docker.com/get-started) sur votre système.  

### Installation avec Docker  
1. Téléchargez l'image officielle Redis :  
   ```bash
   docker pull redis
   ```
2. Lancez un conteneur Redis :
   ```bash
   docker run --name redis-container -d -p 6379:6379 redis
   ```
3. Connectez-vous à la CLI Redis :
   ```bash
   docker exec -it redis-container redis-cli
   ```

## Tester Redis  
Vérifiez que Redis fonctionne correctement en utilisant la commande suivante :  
```bash
docker exec -it my-redis redis-cli
```

## Premiers Pas avec Redis CLI

### Définir une Clé/Valeur  
Redis utilise des paires clé/valeur pour stocker des données simples.

- **Créer une clé :**
  ```bash
  SET demo "Bonjour"
  ```
  Réponse : `OK`

- **Créer une autre clé :**
  ```bash
  SET user:1234 "Ghada"
  ```
  Réponse : `OK`

- **Lire une valeur :**
  ```bash
  GET user:1234
  ```
  Réponse : `"Ghada"`

- **Mettre à jour une clé :**
  ```bash
  SET demo "Bonsoir"
  ```
  Réponse : `OK`

- **Supprimer une clé :**
  ```bash
  DEL user:1234
  ```
  Résultat : `1` (clé supprimée), ou `0` (si la clé n’existe pas).

### Incrémenter un Compteur  
Redis permet d'incrémenter et de décrémenter des valeurs de manière atomique.

- **Initialiser un compteur :**
  ```bash
  SET 1mars 0
  ```

- **Incrémenter le compteur :**
  ```bash
  INCR 1mars
  ```
  Réponse : `1`

- **Décrémenter :**
  ```bash
  DECR 1mars
  ```
  Réponse : `0`

### Expiration d’une Clé  
Les clés peuvent avoir une durée de vie limitée, après laquelle elles sont automatiquement supprimées.

- **Créer une clé :**
  ```bash
  SET maCle "maValeur"
  ```

- **Définir une durée de vie :**
  ```bash
  EXPIRE maCle 120
  ```
  Résultat : `1`

- **Vérifier le temps restant :**
  ```bash
  TTL maCle
  ```
  Résultat : `112`

## Travailler avec d’autres Structures de Données

### Les Listes  
Les listes sont des collections ordonnées d'éléments.

- **Ajouter des éléments :**
  ```bash
  RPUSH mesCours "BDA"
  RPUSH mesCours "Service Web"
  ```

- **Lire les éléments :**
  ```bash
  LRANGE mesCours 0 -1
  ```
  Résultat : `["BDA", "Service Web"]`

- **Supprimer des éléments :**
  ```bash
  RPOP mesCours
  ```
  Par la gauche :
  ```bash
  LPOP mesCours
  ```

### Les Ensembles  
Les ensembles stockent des éléments uniques et non ordonnés.

- **Ajouter des éléments :**
  ```bash
  SADD utilisateurs "Augustin"
  SADD utilisateurs "Ines"
  SADD utilisateurs "Ghada"
  ```

- **Vérifier les membres :**
  ```bash
  SMEMBERS utilisateurs
  ```
  Résultat : `["Augustin", "Ines", "Ghada"]`

- **Supprimer un élément :**
  ```bash
  SREM utilisateurs "Ghada"
  ```
  Résultat : `1`

- **Union de deux ensembles :**
  ```bash
  SADD autreUtilisateurs "Antoine"
  SADD autreUtilisateurs "Farah"
  SUNION utilisateurs autreUtilisateurs
  ```
  Résultat : `["Augustin", "Ines", "Antoine", "Farah"]`

### Ensembles Ordonnés (Sorted Set)  
Utilisés pour classer des éléments par score, idéal pour les systèmes de recommandation.

- **Ajouter des utilisateurs avec des scores :**
  ```bash
  ZADD score4 19 "Augustin"
  ZADD score4 18 "Ines"
  ZADD score4 10 "Samir"
  ZADD score4 8 "Augustin"
  ```

- **Récupérer les éléments par score croissant :**
  ```bash
  ZRANGE score4 0 -1
  ```

- **Récupérer les éléments par score décroissant :**
  ```bash
  ZREVRANGE score4 0 -1
  ```

- **Connaître le rang d'un élément :**
  ```bash
  ZRANK score4 "Augustin"
  ```

### Hashmaps (Hash)  
Permettent de stocker des paires clé/valeur dans une seule clé Redis.

- **Ajouter des informations utilisateur :**
  ```bash
  HSET user:11 username "ghada"
  HSET user:11 age 25
  HSET user:11 email "ghada.malek12@gmail.com"
  ```

- **Récupérer toutes les informations :**
  ```bash
  HGETALL user:11
  ```

- **Ajouter plusieurs champs en une seule ligne :**
  ```bash
  HSET user:4 username "zeineb" age 5 email "zeineb.malek@gmail.com"
  ```

- **Incrémenter l'âge :**
  ```bash
  HINCRBY user:4 age 4
  ```
### HyperLogLog

HyperLogLog est une structure de données probabiliste utilisée pour estimer le nombre d'éléments uniques dans un ensemble, avec une faible utilisation de mémoire.

- **Ajouter des éléments :**
  ```bash
  PFADD visiteurs "Alice" "Bob" "Charlie"
  ```

- **Estimer le nombre d'éléments uniques :**
  ```bash
  PFCOUNT visiteurs
  ```

- **Fusionner plusieurs HyperLogLogs :**
  ```bash
  PFMERGE total_visiteurs visiteurs1 visiteurs2
  ```

HyperLogLog est particulièrement utile pour des analyses rapides où une estimation est suffisante, comme le comptage de visiteurs uniques sur un site web.
## Persistance et Limites de Redis  
Redis stocke les données en mémoire, ce qui peut entraîner des pertes en cas de panne. Il est idéal pour des caches rapides et des données temporaires.

 
