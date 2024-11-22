# Guide d'Introduction à Redis via CLI  
Ce projet propose un guide pratique et détaillé pour découvrir Redis, une base de données NoSQL clé/valeur rapide et performante. Vous apprendrez à installer Redis, à manipuler des données via la CLI, et à explorer ses principales fonctionnalités.  
## Table des Matières  
- [Introduction](#introduction)  
- [Bases de Données SQL et NoSQL](#bases-de-données-sql-et-nosql)  
  - [Approche SQL](#approche-sql)  
  - [Approche NoSQL](#approche-nosql)  
  - [Avantages et Inconvénients](#avantages-et-inconvénients)  
- [Les 4 Familles des Bases de Données NoSQL](#les-4-familles-des-bases-de-données-nosql)  
- [Installation](#installation)  
  - [Prérequis](#prérequis)  
  - [Installation avec Docker](#installation-avec-docker)  
- [Premiers Pas avec Redis CLI](#premiers-pas-avec-redis-cli)  
  - [Commandes Essentielles](#commandes-essentielles)  
- [Structures de Données Redis](#structures-de-données-redis)  
  - [Clés/Valeurs (Key/Value)](#clévaleurs-keyvalue)  
  - [Listes (List)](#listes-list)  
  - [Ensembles (Set)](#ensembles-set)  
  - [Ensembles Ordonnés (Sorted Set)](#ensembles-ordonnés-sorted-set)  
  - [Hashmaps (Hash)](#hashmaps-hash)  
  - [Streams](#nouvelle-structure-streams)  
- [Fonctionnalités Avancées](#fonctionnalités-avancées)  
- [Remarques et Limitations](#remarques-et-limitations)  
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

## Introduction  Redis 

Redis (Remote Dictionary Server) est une base de données NoSQL clé/valeur rapide et légère, conçue pour fonctionner principalement en mémoire. Grâce à ses performances élevées, il est utilisé dans divers scénarios tels que :  
- Le stockage temporaire de sessions utilisateur.  
- La gestion de caches rapides.  
- Les systèmes de recommandation.  

Ce guide vise à rendre Redis accessible, même sans expérience préalable avec les bases de données.  
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
-name redis-container : Donne un nom au conteneur.
-d : Exécute le conteneur en arrière-plan.
-p 6379:6379 : Expose le port Redis par défaut (6379).

 
