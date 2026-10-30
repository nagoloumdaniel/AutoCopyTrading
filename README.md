# AutoCopyTrading

> **Projet en conception : aucun code n'est livré pour l'instant.** Ce dépôt ne contient que la présentation du projet. Le cahier des charges sera ajouté dans `docs/`.

## Avertissement

- **Le trading comporte un risque de perte en capital, pouvant aller jusqu'à la totalité des fonds engagés.**
- Ce projet **ne promet aucune rentabilité** et **ne constitue pas un conseil en investissement**.
- L'IA envisagée n'est pas une garantie de performance : elle ne sert qu'à assister la sélection et la surveillance, sous des garde-fous déterministes.

## Objectif

Concevoir un agent assisté par IA qui analyse les fournisseurs de signaux accessibles via **Deriv MT5**, les classe selon des critères de risque (régularité, perte maximale, stabilité, coûts, qualité des données) et supervise la copie, avec la **préservation du capital** comme priorité.

## Périmètre prévu (version 1)

- Découverte et classement multicritère des traders.
- Détection des stratégies risquées et des comportements suspects.
- Module IA de seconde opinion et de veto.
- Supervision de la copie via les mécanismes natifs et autorisés.
- Limites de perte, contrôle de la marge, arrêt d'urgence.
- Tableau de bord web, notifications Telegram, journal d'audit.
- Backtesting, mode démo, puis mode réel contrôlé.

**Hors périmètre de la v1 :** garantie de rentabilité, contournement des restrictions de Deriv/MT5/MQL5, accès non autorisé aux comptes de tiers, gestion de fonds de tiers, ordres envoyés par un LLM sans contrôles déterministes.

## Architecture cible (prévue, non implémentée)

| Couche | Technologies envisagées |
|---|---|
| Frontend | Next.js, TypeScript, Tailwind CSS |
| Backend / IA | Python (FastAPI), éventuellement Node.js/TypeScript |
| Données | PostgreSQL, Redis (si nécessaire) |
| Trading | Terminal MetaTrader 5 |
| Notifications | Telegram |

Le fournisseur de modèle IA doit rester interchangeable, avec un mode dégradé sans LLM.

## État d'avancement

Phase : **cadrage / spécification**. Aucune fonctionnalité n'est disponible.

## Licence

Aucune licence n'est définie : **tous droits réservés par défaut**. Une licence (MIT pour un projet ouvert, ou licence propriétaire) pourra être choisie plus tard.
