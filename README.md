# Infrastructure Web pour www.foobar.com

Ce document présente les différents éléments d’une infrastructure web complète, sécurisée et surveillée. Il vise à expliquer le rôle de chaque composant et pourquoi il est essentiel dans un environnement de production.

---

## 1. Load Balancer (HAProxy)

### Rôle
Le load balancer (équilibreur de charge) distribue les requêtes des utilisateurs entre plusieurs serveurs pour répartir la charge et améliorer la disponibilité du service.

### Pourquoi est-il utilisé ?
- Pour éviter qu’un seul serveur ne soit surchargé
- Pour assurer la haute disponibilité du site
- Pour améliorer les performances globales en répartissant intelligemment le trafic

---

## 2. Serveur Web (Nginx)

### Rôle
Nginx traite les requêtes HTTP/HTTPS. Il peut :
- Servir les fichiers statiques (HTML, images, CSS, JavaScript)
- Faire office de proxy pour transmettre les requêtes dynamiques vers l’application

### Pourquoi est-il utilisé ?
- Il est rapide, léger et performant
- Il permet la séparation des tâches entre le contenu statique et dynamique
- Il peut gérer le cache, la compression, les redirections, etc.

---

## 3. Serveur d’Application

### Rôle
Le serveur d’application exécute la logique métier du site web (ex. : authentification, gestion des utilisateurs, traitement de formulaires).

### Pourquoi est-il utilisé ?
- Pour centraliser le code métier de l’application
- Pour répondre aux requêtes dynamiques envoyées par les utilisateurs
- Pour interagir avec la base de données

---

## 4. Base de Données (MySQL)

### Rôle
Elle stocke les données persistantes de l’application, comme les comptes utilisateurs, les contenus, les événements, etc.

### Pourquoi est-elle utilisée ?
- Pour organiser et interroger les données de manière structurée
- Pour assurer la pérennité des informations
- Pour permettre des recherches et des traitements rapides via SQL

---

## 5. Pare-feux (Firewalls)

### Rôle
Un pare-feu filtre le trafic réseau entrant et sortant, selon des règles définies.

### Pourquoi sont-ils utilisés ?
- Pour empêcher les connexions non autorisées
- Pour limiter l’exposition des services sensibles
- Pour renforcer la sécurité de l’infrastructure

---

## 6. Certificat SSL / HTTPS

### Rôle
Un certificat SSL permet de chiffrer les communications entre le navigateur de l’utilisateur et le serveur, via le protocole HTTPS.

### Pourquoi est-il utilisé ?
- Pour protéger les données sensibles (mots de passe, formulaires)
- Pour éviter les attaques de type « homme du milieu »
- Pour inspirer confiance à l’utilisateur et améliorer le référencement

---

## 7. Supervision / Monitoring

### Rôle
La supervision consiste à surveiller en temps réel le fonctionnement des serveurs, des applications et de la base de données.

### Pourquoi est-elle utilisée ?
- Pour détecter rapidement les erreurs ou incidents
- Pour anticiper des problèmes de charge ou de performance
- Pour obtenir des statistiques utiles sur le comportement du site

### Exemple de surveillance :
- Suivi des requêtes par seconde (QPS) du serveur web
- Analyse des erreurs retournées par l’application
- Consommation CPU, mémoire, espace disque

---

## Limites et Problèmes Possibles

### Terminaison SSL au niveau du Load Balancer
- Si le SSL est déchiffré au niveau du load balancer et non transmis en HTTPS aux serveurs internes, cela peut poser un problème de sécurité en interne.

### Un seul serveur MySQL en écriture
- Cela crée un point de défaillance unique : si le serveur tombe, l’écriture est impossible.
- Difficile à faire évoluer pour absorber plus de trafic.

### Tous les composants sur un seul serveur
- Si un serveur contient à la fois le serveur web, l’application et la base de données, cela rend l’évolution difficile.
- En cas de panne, tous les services sont touchés.
- La séparation des rôles permet de mieux répartir les ressources et de mieux diagnostiquer les problèmes.

---

## Conclusion

Ces exercices ont permis de comprendre :
- Le rôle de chaque composant d’une infrastructure web
- Les bonnes pratiques pour sécuriser, surveiller et faire évoluer une architecture
- L’importance de la séparation des rôles, du chiffrement, et de la supervision

Ce socle de connaissances est essentiel pour construire des applications web robustes, performantes et sécurisées.

