# UtilityLab

UtilityLab est un projet de plateforme d'entraînement communautaire pour Counter-Strike 2.

L'objectif du projet est de créer un environnement moderne, performant et évolutif permettant aux joueurs de :

* apprendre les utilitaires
* sauvegarder des lineups
* partager des smokes
* rejouer des actions
* progresser
* participer à une communauté compétitive
* s'entraîner en groupe
* coacher d'autres joueurs
* utiliser plusieurs serveurs synchronisés

---

# Vision du Projet

UtilityLab n'est pas un simple serveur practice.

Le projet vise à devenir une véritable plateforme communautaire autour des utilitaires CS2.

Le serveur doit permettre :

* entraînement individuel
* entraînement d'équipe
* coaching
* partage communautaire
* progression joueur
* création de contenu
* compétition sociale
* système de réputation
* leaderboard
* validation communautaire

L'objectif principal :

> Créer la meilleure plateforme CS2 pour apprendre, partager et maîtriser les utilitaires.

---

# Philosophie Technique

Le projet privilégie :

* stabilité
* architecture propre
* modularité
* performances
* maintenabilité long terme
* faible couplage
* évolutivité multi-serveurs

Règle principale :

> Architecture first, features second.

Le projet doit éviter :

* code spaghetti
* dépendances inutiles
* UI lourdes
* systèmes non maintenables
* couplage fort entre modules
* logique métier directement dans l'UI

---

# Stack Technique

## Serveur

### Développement

* Windows local
* SteamCMD
* Counter-Strike 2 Dedicated Server

### Production

* Linux dédié / VPS
* multi-instances
* orchestration possible plus tard

---

## Framework Plugin

* Metamod
* CounterStrikeSharp
* .NET 8
* C#

---

## UI

Le projet utilisera principalement :

* CS2MenuManager
* Numeric ScreenMenu
* navigation clavier 1 → 0

Style de menu souhaité :

```txt
1. Option
2. Option
3. Option

0. Retour
```

Le projet évite volontairement :

* Panorama complexe
* UI HTML lourdes
* overlays permanents
* menus souris obligatoires

Philosophie UI :

> Gameplay first.

L'UI doit être :

* rapide
* légère
* stable
* efficace
* utilisable sans quitter le gameplay

---

## Storage

### Développement

* SQLite

### Production

* PostgreSQL

### Plus tard

* Redis

Redis pourra servir pour :

* cache
* synchronisation rapide
* sessions
* communication multi-serveurs
* matchmaking d'instances

---

# Architecture du Projet

```txt
UtilityLab/
├─ src/
│  └─ UtilityLab/
│     ├─ Core/
│     ├─ Commands/
│     ├─ UI/
│     ├─ Practice/
│     ├─ Bots/
│     ├─ Replay/
│     ├─ Lineups/
│     ├─ Coach/
│     ├─ Storage/
│     ├─ Config/
│     ├─ Analytics/
│     └─ Networking/
├─ tests/
├─ docs/
├─ tools/
├─ assets/
└─ scripts/
```

---

# Décisions Techniques Importantes

## Les lineups ne sont PAS de simples positions

Une lineup est considérée comme :

> Une séquence gameplay enregistrée.

Le système doit être pensé dès le départ pour supporter :

* stand throw
* jumpthrow
* W+jumpthrow
* runthrow
* crouch throw
* run+jumpthrow
* ghost replay
* playback
* coaching
* validation automatique

---

## Le système doit être tick-based

Le replay et les lineups doivent être :

* tick-based
* déterministes
* précis

Et NON :

* time-based uniquement

---

## Les lineups doivent enregistrer

* position
* angle
* grenade utilisée
* inputs joueur
* timings
* mouvements
* saut
* crouch
* release grenade
* metadata communautaires

---

## Les actions doivent être enregistrées

Exemple :

```json
{
  "tick": 12,
  "type": "MOVE_FORWARD",
  "value": 1.0
}
```

Actions prévues :

* MOVE_FORWARD
* MOVE_BACKWARD
* MOVE_LEFT
* MOVE_RIGHT
* JUMP
* DUCK
* ATTACK
* ATTACK2
* RELEASE
* STOP_MOVE

---

# Philosophie Multi-Serveurs

Le projet ne doit PAS utiliser une mega-map fusionnant toutes les maps compétitives.

Décision officielle :

> 1 map = 1 serveur.

Architecture finale visée :

```txt
Hub
├─ Mirage
├─ Inferno
├─ Nuke
├─ Ancient
├─ Dust2
├─ Anubis
└─ Vertigo
```

Tous les serveurs partageront :

* comptes joueurs
* lineups
* statistiques
* favoris
* progression
* réputation
* leaderboards

via PostgreSQL.

---

# Système Communautaire

Le projet doit fortement encourager la contribution des joueurs.

---

## Likes / Votes

Les joueurs doivent pouvoir :

* liker
* downvote
* favorite
* partager
* sauvegarder

les lineups.

---

## Validation Communautaire

Statuts prévus :

```txt
Pending
→ Approved
→ Verified
```

---

## Créateurs

Le projet doit permettre de mettre en avant :

* top creators
* meilleurs coachs
* meilleures lineups
* lineups populaires

---

# Système de Progression

Le serveur doit proposer :

* XP
* niveaux
* statistiques
* rangs
* progression par map
* progression par utilitaire
* challenges
* leaderboards

---

## Exemple de progression

```txt
+5 XP smoke réussie
+20 XP lineup validée
+50 XP lineup populaire
```

---

## Leaderboards

Prévisions :

* meilleurs joueurs Mirage
* meilleurs créateurs
* meilleures flashes
* meilleures smokes
* accuracy
* fastest execute
* most used lineups

---

# Fonctionnalités Principales

## Practice

* infinite utility
* no reload
* bunnyhop
* noclip
* grenade trajectory
* replay grenade
* impacts
* utility clear
* practice settings

---

## Bots

* placement exact
* freeze
* invincible
* ownership
* cleanup ciblé
* presets

---

## Replay

* replay de lineup
* ghost trajectory
* playback inputs
* coach replay
* slow motion
* comparaison de lineups

---

## Coach

* freeze joueurs
* démonstration
* replay partagé
* téléportation
* observation
* correction timing

---

## Analytics

Prévoir dès le début :

* lineups populaires
* maps populaires
* lineups ratées
* temps d'exécution
* taux de réussite
* statistiques joueurs

---

# Web Panel (Plus tard)

Le projet prévoit plus tard un web panel permettant :

* administration
* validation des lineups
* gestion des tags
* analytics
* gestion serveurs
* monitoring
* gestion utilisateurs
* modération

L'administration lourde ne sera pas faite directement in-game.

---

# Roadmap

# Phase 1 — Base Serveur

Objectif :

Créer un serveur local stable et maintenable.

Checklist :

* [ ] installer SteamCMD
* [ ] installer serveur CS2
* [ ] créer scripts de lancement
* [ ] créer scripts d'update
* [ ] préserver gameinfo.gi pour Metamod
* [ ] installer Metamod
* [ ] installer CounterStrikeSharp
* [ ] charger plugin test

---

# Phase 2 — Base Plugin

Objectif :

Créer une base plugin propre et modulaire.

Checklist :

* [ ] solution .NET
* [ ] plugin UtilityLab vide
* [ ] logger
* [ ] config loader
* [ ] command manager
* [ ] player session manager
* [ ] storage abstraction
* [ ] UI abstraction
* [ ] event pipeline

---

# Phase 3 — Practice V0.1

Objectif :

Créer une première version jouable.

Checklist :

* [ ] /prac
* [ ] /noclip
* [ ] /clear
* [ ] /rethrow
* [ ] /placebot
* [ ] ownership des entités
* [ ] infinite utility
* [ ] sessions joueur

---

# Phase 4 — Replay & Lineups

Checklist :

* [ ] modèle de lineup
* [ ] stockage inputs
* [ ] stockage tick-based
* [ ] sauvegarde lineups
* [ ] chargement lineups
* [ ] replay simple
* [ ] playback
* [ ] favoris
* [ ] tags

---

# Phase 5 — UI

Checklist :

* [ ] menu principal
* [ ] sous-menus
* [ ] menu lineups
* [ ] menu bots
* [ ] menu coach
* [ ] fallback commandes chat

---

# Phase 6 — Communautaire

Checklist :

* [ ] likes
* [ ] votes
* [ ] validation
* [ ] profils créateurs
* [ ] réputation
* [ ] progression
* [ ] leaderboards
* [ ] challenges

---

# Phase 7 — Multi-Serveurs

Checklist :

* [ ] PostgreSQL
* [ ] hub
* [ ] serveurs par map
* [ ] synchronisation
* [ ] monitoring
* [ ] backups
* [ ] logs centralisés

---

# Commandes Prévues

```txt
/prac
/lineups
/save
/load
/placebot
/removebot
/clear
/rethrow
/noclip
/coach
/share
/favorite
/like
/vote
```

---

# Principes de Code

Le code ne doit jamais :

* coupler UI et logique métier
* accéder directement à SQLite partout
* dépendre d'une seule implémentation menu
* stocker les lineups comme de simples positions
* créer des managers globaux incontrôlés
* ignorer l'ownership des entités

Le code doit utiliser :

* interfaces
* services
* abstraction
* cleanup systématique
* logs explicites
* configuration centralisée
* architecture modulaire

---

# État Actuel

```txt
Statut : setup serveur local en cours
Dernière étape : téléchargement CS2 Dedicated Server
Prochaine étape : premier lancement vanilla
```

---

# Notes

Le projet doit rester compatible avec une évolution future vers :

* plateforme multi-serveurs
* replay avancé
* ghost systems
* coaching avancé
* matchmaking d'entraînement
* analytics avancés
* web panel complet
* instances dynamiques
