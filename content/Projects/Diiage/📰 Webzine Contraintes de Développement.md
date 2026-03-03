
> [!info] 📌 Contexte
> Note de synthèse des **contraintes officielles** du projet Webzine (CCTP Dév + Note de cadrage).  
> Cette note sert de référence technique pour garantir la conformité des livrables.

---

## 🧭 Overview

Le projet **Webzine** impose un cadre technique strict :

- Stack technologique imposée
- Architecture en couches obligatoire
- Support multi-SGBD
- Respect strict des conventions
- Livrable exécutable sans modification

L’objectif est d’assurer :
- Maintenabilité
- Performance
- Testabilité
- Industrialisation du projet

---

## ⚙️ Contraintes Techniques et Frameworks

> [!warning] Obligatoire – Toute non-conformité peut invalider le livrable

### 🔹 Framework

- **ASP.NET Core 10.0 (LTS)** → Version impérative

### 🔹 Navigateurs supportés

- Chromium (desktop & mobile)
- Firefox (desktop & mobile)
- Edge (desktop & mobile)

### 🔹 Performance

- Temps de chargement maximal : **< 1 seconde**
- Hypothèse réseau : **1 Mo/s**

### 🔹 Journalisation

- Librairie imposée : **nLog**
- Logs applicatifs structurés
- Pas d’implémentation custom maison

---

## 🏗️ Méthodologie de Développement

> [!tip] L’architecture est un critère majeur d’évaluation

### 🔹 Approche

- **Code First obligatoire**

### 🔹 Architecture en couches

Structure minimale exigée :

```csharp
Webzine.Business  
Webzine.Business.Contracts  
Webzine.Documentation
Webzine.Entity  
Webzine.EntitiesContext  
Webzine.Entity.Tests
Webzine.Repository  
Webzine.Repository.Contracts
Webzine.WebApplication  
```

> [!danger] Aucun mélange de responsabilités entre couches

### 🔹 Repositories

Les interfaces sont à placer dans le projet `Webzine.Repository.Contracts`.

#### IArtisteRepository
| Fonctionnalité | Signature |
| :--- | :--- |
| Ajoute un nouvel artiste. | `void Add(Artiste artiste);` |
| Supprime un artiste. | `void Delete(Artiste artiste);` |
| Retourne l’artiste demandé. | `Artiste Find(int id);` |
| Retourne tous les artistes. | `IEnumerable<Artiste> FindAll();` |
| Met à jour un artiste. | `void Update(Artiste artiste);` |
#### ITitreRepository
| Fonctionnalité | Signature |
| :--- | :--- |
| Ajoute un nouveau titre. | `void Add(Titre titre);` |
| Compte le nombre de titres. | `int Count();` |
| Supprime un titre. | `void Delete(Titre titre);` |
| Retourne le titre demandé à partir de son identifiant. | `Titre Find(int idTitre);` |
| Retourne les titres demandés (pour la pagination) triés selon la date de création (du plus récent à ancien). | `IEnumerable<Titre> FindTitres(int offset, int limit);` |
| Retourne tous les titres. | `IEnumerable<Titre> FindAll();` |
| Incrémente le nombre de lectures d’un titre. | `void IncrementNbLectures(Titre titre);` |
| Incrémente le nombre de likes d’un titre. | `void IncrementNbLikes(Titre titre);` |
| Recherche, de manière insensible à la casse, les titres contenant le mot cherché. | `IEnumerable<Titre> Search(string mot);` |
| Recherche, de manière insensible à la casse, les titres contenant le style de musique cherché. | `IEnumerable<Titre> SearchByStyle(string libelle);` |
| Met à jour un titre. | `void Update(Titre titre);` |
#### IStyleRepository
| Fonctionnalité | Signature |
| :--- | :--- |
| Ajoute un nouveau style de musique. | `void Add(Style style);` |
| Supprime un style de musique. | `void Delete(Style style);` |
| Retourne le style de musique demandé. | `Style Find(int id);` |
| Retourne tous les styles de musique. | `IEnumerable<Style> FindAll();` |
| Met à jour un style de musique. | `void Update(Style style);` |
#### ICommentaireRepository
| Fonctionnalité | Signature |
| :--- | :--- |
| Ajoute un nouveau commentaire. | `void Add(Commentaire commentaire);` |
| Supprime un commentaire. | `void Delete(Commentaire commentaire);` |
| Retourne le commentaire demandé. | `Commentaire Find(int id);` |
| Retourne tous les commentaires. | `IEnumerable<Commentaire> FindAll();` |

Contraintes :
- Respect strict des signatures fournies
- Implémentation propre et testable

---

## 💾 Persistance et Données

### 🔹 Modes de stockage configurables

Configuration via `appsettings.json`

1. **Local**
   - Données en dur (bouchonnage)
   - Phase initiale uniquement

2. **Base de données**
   - SQLite → Obligatoire pour les livrables
   - PostgreSQL → Production
   - SQL Server → Production

> [!important] Le projet doit fonctionner immédiatement avec SQLite

---

### 🔹 Seeding (Initialisation)

Deux modes obligatoires :

- `SeedDataLocal`
- `SeedDataSpotify`

Les deux doivent être implémentés et sélectionnables.

---

## 🎨 Interface Utilisateur (Frontend)

### 🔹 Framework CSS

- **Bootstrap 5.3.8**
- Fichiers `.min` uniquement
- Aucune modification de la librairie

### 🔹 Responsive Design

- Fidèle aux maquettes
- Adapté mobile & desktop
- Simplicité pour grand public

### 🔹 Icônes

- Font Awesome
  **ou**
- Bootstrap Icons

### 🔹 JavaScript

- Aucun JS attendu
- Si nécessaire → minimal
- Centralisé dans `app.js`

> [!warning] Pas de scripts inline

---

## 🧪 Qualité du Code et Tests

### 🔹 Règles générales

- Pas de code mort
- Pas de code commenté inutile
- Pas de CSS inline
- Variables explicites

### 🔹 Tests unitaires

- Framework : **MSTest**
- Interdiction formelle de modifier :
  - Tests fournis pour les entités

### 🔹 Outils obligatoires

- **StyleCop** → règles de codage
- **Prettier** → formatage Markdown

---

## 📌 Exigences Spécifiques

### 🔹 Routing

Routes imposées (exemples) :

#### Routes Publiques
| Fonctionnalité | Route | Méthode HTTP |
| :--- | :--- | :--- |
| Page d’accueil (liste des titres chroniqués) | `/` | `GET` |
| Page d’accueil (pagination) | `/page/1` | `GET` |
| Page contact | `/contact/` | `GET` |
| Consulter la page d’un artiste | `/artiste/Queen` | `GET` |
| Consulter le titre id=1 | `/titre/1` | `GET` |
| Consulter le titre id=1 (bonus) | `/titre/1/Queen/Bohemian%20Rhapsody` | `GET` |
| Titres selon le style de musique demandé | `/titres/style/jazz/` | `GET` |
| Ajouter un commentaire | `/titre/commenter` | `POST` |
| Liker | `/titre/liker` | `POST` |
| Recherche d’artistes / titres | `/recherche/` | `POST` |
#### Routes API
| Fonctionnalité | Route | Méthode HTTP |
| :--- | :--- | :--- |
| API version | `/api/version` | `GET` |
#### Routes d'Administration
| Fonctionnalité | Route | Méthode HTTP |
| :--- | :--- | :--- |
| **Administration des artistes** | | |
| Liste des artistes | `/administration/artistes/` | `GET` |
| Créer un artiste | `/administration/artiste/create` | `GET` / `POST` |
| Supprimer un artiste | `/administration/artiste/delete/1` | `GET` / `POST` |
| Éditer un artiste | `/administration/artiste/edit/1` | `GET` / `POST` |
| **Administration des titres** | | |
| Liste des titres | `/administration/titres/` | `GET` |
| Créer un titre | `/administration/titre/create` | `GET` / `POST` |
| Supprimer un titre | `/administration/titre/delete/1` | `GET` / `POST` |
| Éditer un titre | `/administration/titre/edit/1` | `GET` / `POST` |
| **Administration des styles de musique** | | |
| Liste des styles | `/administration/styles/` | `GET` |
| Créer un style | `/administration/style/create` | `GET` / `POST` |
| Supprimer un style | `/administration/style/delete/1` | `GET` / `POST` |
| Éditer un style | `/administration/style/edit/1` | `GET` / `POST` |
| **Administration des commentaires** | | |
| Liste des commentaires | `/administration/commentaires/` | `GET` |
| Supprimer un commentaire | `/administration/commentaire/delete/1` | `GET` / `POST` |
| **Tableau de bord** | `/administration/dashboard/` | `GET` |
> **Note :** Si d’autres paginations sont implémentées, il peut être judicieux de faire comme pour les titres paginés en page d’accueil pour rester homogène, c’est-à-dire en employant `/page/x` dans l’URL.

> [!danger] Les routes doivent correspondre exactement aux spécifications

---

### 🔹 API Version

Pour superviser le numéro de version déployée, une API Version doit être implémentée.

Elle doit retourner :

```json
{
	"nom": "webzine",
	"version": "1.0"
}
```

La version vaudra respectivement 1.0, 2.0 et 3.0 pour les jalons n°1, 2 et 3.

---

### 🔹 Livrables

Le projet doit :

- Compiler sous **Visual Studio 2026**
    
- Fonctionner immédiatement avec SQLite
    
- Ne nécessiter aucune modification manuelle
    

---

## 🧩 Customization and Configuration

Configuration centralisée dans :

```csharp
appsettings.json
```

Permet de définir :

- Mode de stockage
    
- Chaîne de connexion
    
- Paramètres de seeding
    

---

## 🔗 Related

- Architecture en couches
    
- Clean Architecture
    
- Code First (Entity Framework)
    
- Repository Pattern
    
- Dependency Injection ASP.NET Core
    

---

## 🌍 Explore More

- Optimisation des performances ASP.NET
    
- Bonnes pratiques EF Core
    
- Stratégies de seeding avancées
    
- Tests unitaires et mocks Repository
    
- Logging structuré et monitoring
    

---

## 📚 Tags

#webzine  #aspnet  #architecture  #code-first  #repository-pattern  #bootstrap  #sqlite  #mstest  #stylecop  #nlog