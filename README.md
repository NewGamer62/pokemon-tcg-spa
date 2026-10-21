# ⚡ Pokémon TCG SPA — Real-Time Multiplayer Card Game

<p align="center">
  <img src="https://img.shields.io/badge/Vue.js-3.5%2B-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white" alt="Vue 3" />
  <img src="https://img.shields.io/badge/TypeScript-5.6%2B-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Vite-5.4-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/Pinia-2.2-FFD859?style=for-the-badge&logo=pinia&logoColor=black" alt="Pinia" />
  <img src="https://img.shields.io/badge/Socket.io-4.8-010101?style=for-the-badge&logo=socketdotio&logoColor=white" alt="Socket.io" />
  <img src="https://img.shields.io/badge/UI-Naive%20UI-18A058?style=for-the-badge" alt="Naive UI" />
  <img src="https://img.shields.io/badge/Docker-Backend%20Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Tests-34%20Passed-brightgreen?style=for-the-badge" alt="Tests" />
  <img src="https://img.shields.io/badge/Projet-BUT%20Informatique-blueviolet?style=for-the-badge" alt="BUT Informatique" />
</p>

---

## 📌 Présentation

**Pokémon TCG SPA** est une application web moderne (Single Page Application) développée en **Vue 3**, **TypeScript** et **WebSockets (Socket.io)** reproduisant fidèlement l'expérience d'un jeu de cartes à collectionner Pokémon en ligne.

L'application intègre un cycle complet d'interaction joueur :

1. **Authentification sécurisée** (JWT, session persistante et guards de navigation).
2. **Atelier de Deck Building** avec gestion de decks de 10 cartes, moteur de recherche instantané sans latence et prévisualisation haute fidélité.
3. **Arène multijoueur temps réel** synchronisée par WebSockets avec matchmaking, gestion du tour par tour, pioche, attaques élémentaires et calcul des conditions de victoire.

🎨 **Maquettes graphiques de référence :** [Consulter le prototype Figma](https://making-rerun-61323218.figma.site/)

---

## ✨ Fonctionnalités Majeures

### ⚔️ Duels Temps Réel & Matchmaking (Socket.io)

- **Lobby en direct** : Rejoindre ou créer une file d'attente multijoueur avec sélection préalable de son deck.
- **Plateau de jeu interactif** : Zone active, banc, main du joueur masquée à l'adversaire et affichage dynamique des points de vie (PV).
- **Moteur de règles & contraintes** :
  - Validation stricte des tours de jeu.
  - Pioche limitée à 5 cartes en main maximum.
  - Exécution des attaques élémentaires avec calcul des faiblesses/résistances et animation des K.O.
  - Détection automatique de fin de partie au bout de 3 K.O. avec modal récapitulatif.

### 🎴 Deck Builder & Gestionnaire de Cartes

- **Création, édition et suppression de decks** de 10 cartes Pokémon.
- **Moteur de recherche temps réel** :
  - Filtrage instantané insensible à la casse et aux diacritiques (accents).
  - Préservation de la sélection active même lors des recherches filtrées.
  - Filtre dédié affichant uniquement les cartes sélectionnées.
- **Optimisation réseau & Cache partagé** : Déduplication de requêtes en vol (_promise deduplication_) et cache mémoire évitant tout rechargement superflu du catalogue de cartes.
- **Aperçu miniature haute définition** des cartes au sein de la liste des decks.

### 📱 Responsive Design & Architecture UI

- Interface entièrement responsive adaptée du mobile au grand écran desktop.
- Composants riches alimentés par **Naive UI** (formulaires, modales, grilles adaptatives, loaders).
- Thème dynamique avec calcul automatique des couleurs élémentaires (Feu, Eau, Plante, Électrique, etc.).

---

## 🛠️ Stack Technique

| Domaine                  | Technologies                                                                               |
| :----------------------- | :----------------------------------------------------------------------------------------- |
| **Framework Core**       | **Vue 3.5** (Composition API, `<script setup>`)                                            |
| **Typage**               | **TypeScript 5.6** (Contrats stricts pour modèles, cartes, decks et events WebSocket)      |
| **Bundler & Tooling**    | **Vite 5.4**, ESLint, Prettier                                                             |
| **State Management**     | **Pinia 2.2** (Stores découplés : `auth.store.ts`, `game.store.ts`)                        |
| **Routage**              | **Vue Router 4** (Navigation guards RG2/RG3 protégés par JWT)                              |
| **Composants UI**        | **Naive UI** (Composants natifs performants sans overhead)                                 |
| **Réseau & Temps Réel**  | **Socket.io Client** (Événements bidirectionnels en duplex intégral) + Composable `useApi` |
| **Backend & Base (Dev)** | **Node.js**, **Express**, **Socket.io**, **PostgreSQL** orchestrés sous **Docker Compose** |
| **Assurance Qualité**    | **Node.js Native Test Runner** (34 tests unitaires & intégration)                          |

---

## 🏗️ Structure du Projet

```
pokemon-tcg-spa/
├── src/
│   ├── components/
│   │   ├── cards/          # Cartes Pokémon individuelles, grilles et badges
│   │   ├── decks/          # Formulaires, sélection et explorateur de decks
│   │   ├── game/           # Plateau de jeu, lobby, main, actions et modale de fin
│   │   └── layout/         # HeaderBar, navigation et profil utilisateur
│   ├── composables/        # useApi, useColors, useDecks, useStorage
│   ├── pages/              # Vues : Home, Auth, DeckDetail/Edit, Game
│   ├── stores/             # Stores Pinia (auth, game)
│   ├── types/              # Définitions TypeScript complètes (carte, deck, jeu, socket)
│   └── utils/              # Logique métier pure (règles de jeu, validation deck, calculs PV)
├── tests/                  # Suites de tests automatisés (decks.test.mjs, game.test.mjs)
├── docker-compose.yml      # Stack backend complète (API + Base de données)
└── vite.config.ts          # Configuration de compilation et alias de chemins
```

---

## 🚀 Démarrage Rapide

### Prérequis

- **Node.js 24+** (ou via nvm : `nvm use 24`)
- **Docker Desktop** (pour faire tourner le backend local)

### 1. Cloner le dépôt

```bash
git clone https://github.com/NewGamer62/pokemon-tcg-spa.git
cd pokemon-tcg-spa
```

### 2. Installer les dépendances

```bash
npm install
```

### 3. Lancer le backend et la base de données (Docker)

```bash
npm run api:start
```

> Démarre automatiquement PostgreSQL sur le port `5432` et l'API Socket.io sur `http://localhost:3001` avec les cartes et utilisateurs pré-configurés.  
> _Documentation Swagger interactive disponible sur : `http://localhost:3001/api-docs`._

### 4. Démarrer le serveur de développement

```bash
npm run dev
```

L'application est immédiatement accessible sur **http://localhost:5173**.

---

## 🧪 Comptes de Test (Seed Inclus)

Après initialisation du backend Docker, deux comptes joueurs prêts à l'emploi sont disponibles pour tester le matchmaking en duel :

| Identifiant | Email              | Mot de passe  |
| :---------- | :----------------- | :------------ |
| **Red**     | `red@example.com`  | `password123` |
| **Blue**    | `blue@example.com` | `password123` |

_Vous pouvez également créer de nouveaux comptes directement depuis la page d'inscription._

---

## 📋 Commandes Disponibles

```bash
npm run dev          # Démarrer le serveur Vite local
npm run build        # Compiler pour la production (TypeScript + bundling Vite)
npm test             # Exécuter les 34 tests unitaires et d'intégration
npm run lint         # Analyse statique ESLint
npm run api:start    # Démarrer le backend Docker (API REST + Socket.io)
npm run api:stop     # Arrêter le backend Docker
npm run api:reset    # Réinitialiser la base de données à blanc (re-seed)
```

---

## 🎓 Contexte Académique

Projet réalisé par **Noa Gaillard** (`NewGamer62`) dans le cadre de la **SAÉ Développement Web Avancé** (BUT Informatique, IUT de Lens).  
Conception d'une architecture frontend temps réel complète conforme aux exigences professionnelles d'accessibilité, de typage strict et de performance réseau.
