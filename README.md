# UtilityLab

UtilityLab est un projet de serveur d'entraînement CS2 dédié aux utilitaires, aux lineups, au coaching et à la progression communautaire.

L'objectif est de créer une plateforme stable, performante et évolutive où les joueurs peuvent apprendre, sauvegarder, partager, noter et rejouer des lineups sur les maps compétitives de Counter-Strike 2.

---

## Objectif du projet

UtilityLab n'est pas un simple serveur practice.

Le projet vise à combiner :

- entraînement utilitaire
- lineups sauvegardées
- replay de grenades
- bots d'entraînement
- progression joueur
- leaderboards
- votes et likes communautaires
- coaching multi-joueurs
- persistance multi-serveurs

---

## Stack technique prévue

### Serveur

- Counter-Strike 2 Dedicated Server
- Environnement local Windows pour le développement
- Environnement Linux prévu pour la production

### Framework plugin

- Metamod
- CounterStrikeSharp
- C# / .NET 8

### Stockage

- SQLite en développement local
- PostgreSQL en production multi-serveurs
- Redis optionnel plus tard pour cache / sessions / synchronisation rapide

### UI

- Menus in-game type numérique 1 à 0
- Abstraction UI pour pouvoir changer de système de menu sans modifier la logique métier
- Web panel prévu plus tard pour l'administration lourde

---

## Philosophie de développement

Le projet privilégie :

- stabilité avant quantité de features
- architecture modulaire
- faible couplage
- responsabilités claires
- compatibilité multi-serveurs
- performances serveur
- maintenabilité long terme

Règle principale :

> Architecture first, features second.

---

## Architecture prévue

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
│     └─ Analytics/
├─ tests/
├─ docs/
├─ tools/
└─ assets/